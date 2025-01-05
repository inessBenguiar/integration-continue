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
                echo 'Tests complete.'
            }
        }
        stage('SonarQube Analysis') {
                    steps {
                        withSonarQubeEnv('SonarQube') {
                            bat './gradlew sonarqube'
                        }
                    }
                }
    }
}
