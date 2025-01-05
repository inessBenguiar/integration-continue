pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                bat './gradlew test'
                archiveArtifacts 'build/test-results/'

                cucumber(
                    reportTitle: 'My report',
                    fileIncludePattern: 'build/reports/example-report.json',
                    trendsLimit: 10,
                    classifications: [
                        [
                            'key': 'Browser',
                            'value': 'Firefox'
                        ]
                    ]
                )

                echo 'Tests complete.'
            }
        }
    }
}
