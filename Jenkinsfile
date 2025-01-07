pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                bat './gradlew test'
                archiveArtifacts artifacts: 'build/test-results/', allowEmptyArchive: true
                cucumber(
                    reportTitle: 'My report',
                    fileIncludePattern: 'reports/example-report.json',
                    trendsLimit: 10,
                    classifications: [
                        [
                            'key': 'Browser',
                            'value': 'Firefox'
                        ]
                    ]
                )
                junit 'build/test-results/test/TEST-Matrix.xml'
            }
        }
        stage('Code Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    bat './gradlew sonarqube'
                }
            }
        }

        stage('Code Quality') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }

        stage('Build') {
            steps {
                bat './gradlew.bat build'
                bat './gradlew.bat javadoc'
                archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: true
                archiveArtifacts artifacts: 'build/docs/', allowEmptyArchive: true
            }
        }
        stage('Deploy') {
            steps {
                bat './gradlew.bat publish'
            }
        }
        stage('Notify') {
            steps {
                script {
                    slackSend(
                        channel: '#integration-continue-jenkins',
                        message: "Build and deployment successful: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
                    )
                    emailext(
                        subject: "SUCCESS: Application Deployed Successfully" ,
                        body: "The application was deployed successfully." ,
                        to: 'is_benguiar@esi.dz'
                    )
                }
            }
        }
    }

    post {
        failure {
            steps {
                slackSend(
                    channel: '#integration-continue-jenkins',
                    message: "Build or deployment failed: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
                )
                emailext(
                    subject: "FAILURE: Application did not Deploye" ,
                    body: "The application was not deployed." ,
                    to: 'is_benguiar@esi.dz'

                )
            }
        }
    }
}
