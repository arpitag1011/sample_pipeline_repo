pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" install'
            }
        }

        stage('Test') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying React App...'
            }
        }
    }
}
