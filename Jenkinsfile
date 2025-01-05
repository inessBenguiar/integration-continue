pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
            bat './gradlew test'
            archiveArtifacts 'build/test-results/'
            // cucumber buildStatus: 'UNSTABLE',
                    reportTitle: 'My report',
                    fileIncludePattern: 'target/cucumber.json',
                    trendsLimit: 10,
                    classifications: [
                        [
                            'key': 'Browser',
                            'value': 'Firefox'
                        ]
                    ]
                echo 'Tests complete.'
            }
        }

    }
}
