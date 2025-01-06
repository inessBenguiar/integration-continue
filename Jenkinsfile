pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                bat './gradlew test'
                archiveArtifacts 'build/test-results/'
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
        /*
        stage('Code Quality') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
        */
        stage('Build') {
            steps {
                bat './gradlew.bat build'
                bat './gradlew.bat javadoc'
                archiveArtifacts 'build/libs/*.jar'
                archiveArtifacts 'build/docs/'
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
                    if (currentBuild.currentResult == 'SUCCESS') {
                        slackSend(
                            channel: '#integration-continue-jenkins',
                            message: "✅ Build and deployment successful: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)",
                            color: 'good'
                        )
                    } else {
                        slackSend(
                            channel: '#integration-continue-jenkins',
                            message: "❌ Build or deployment failed: ${env.JOB_NAME} #${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)",
                            color: 'danger'
                        )
                    }
                }
            }
        }
    }
}
