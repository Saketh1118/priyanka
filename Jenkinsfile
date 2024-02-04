pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from the repository
                script {
                    checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                // Build your application
                script {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                // Run tests for your application
                script {
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            when {
                // Only deploy on the master branch
                expression { 
                    return env.BRANCH_NAME == 'master'
                }
            }
            steps {
                // Deploy your application (adjust as needed)
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }

    post {
        success {
            // Actions to be taken on successful build
            echo 'Deployment successful!'
        }
        failure {
            // Actions to be taken on build failure
            echo 'Deployment failed!'
        }
    }
}

