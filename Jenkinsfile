pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
            bat './gradlew test'
                // Simulate running tests with a print statement
                echo 'Tests complete.'
            }
        }

    }
}
