pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Vous pouvez ajouter des commandes pour construire votre projet ici
                sh 'echo "Building project..."'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Vous pouvez ajouter des commandes pour exécuter vos tests ici
                sh 'echo "Running tests..."'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the project...'
                // Ajoutez ici des étapes pour déployer votre application
                sh 'echo "Deploying project..."'
            }
        }
    }
}