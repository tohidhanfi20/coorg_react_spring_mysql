pipeline {
    agent any

    environment {
        GIT_CRED = 'git-cred' // GitHub token credentials ID
    }

    stages {
        stage('Checkout Code from GitHub') {
            steps {
                // Checkout code from GitHub
                git credentialsId: "${GIT_CRED}", url: 'https://github.com/tohidhanfi20/coorg_react_spring_mysql.git', branch: 'main'
            }
        }

        stage('Build and Run Frontend') {
            steps {
                script {
                    // Build frontend Docker image
                    docker.build('frontend-image', './frontend')

                    // Run the frontend container
                    docker.image('frontend-image').run('-d -p 8080:80')
                }
            }
        }

        stage('Build and Run Backend') {
            steps {
                script {
                    // Build backend Docker image
                    docker.build('backend-image', './backend')

                    // Run the backend container
                    docker.image('backend-image').run('-d -p 8081:8081')
                }
            }
        }
    }
}
