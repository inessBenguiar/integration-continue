pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
            bat './gradlew test'
            archiveArtifacts 'build/test-results/'
                echo 'Tests complete.'
            }
        }

    }
}
