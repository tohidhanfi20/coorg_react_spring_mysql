pipeline {
    agent any
    
    environment {
        GIT_CRED = 'git-cred' // Set your GitHub credentials ID here
    }
    
    stages {
        stage('Checkout Code from GitHub') {
            steps {
                // Checkout frontend and backend code from GitHub
                git credentialsId: "${GIT_CRED}", url: 'https://github.com/tohidhanfi20/SpringBoot-APP.git', branch: 'main'
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                script {
                    // Build the frontend Docker image
                    docker.build('frontend-image', './frontend')
                }
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                script {
                    // Build the backend Docker image
                    docker.build('backend-image', './backend')
                }
            }
        }

        stage('Run Frontend Docker Container') {
            steps {
                script {
                    // Run frontend container
                    docker.run('frontend-image', '-d -p 8080:80')
                }
            }
        }

        stage('Run Backend Docker Container') {
            steps {
                script {
                    // Run backend container
                    docker.run('backend-image', '-d -p 8081:8081')
                }
            }
        }

        stage('Verify Application') {
            steps {
                script {
                    // Check if frontend and backend are running (this can be enhanced with more checks)
                    sh 'curl http://localhost:8080'  // Frontend check
                    sh 'curl http://localhost:8081'  // Backend check
                }
            }
        }
    }
}
