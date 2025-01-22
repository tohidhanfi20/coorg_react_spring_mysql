pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Use the name you configured in the tools
    }

    
    stage('Provide File Permissions') {
        steps {
            echo 'Installing npm and setting up permissions for build_frontend.sh'
            // Check if the file exists before applying chmod
            sh '''
            if [ -f build_frontend.sh ]; then
                echo "File build_frontend.sh exists. Applying permissions."
                chmod +x build_frontend.sh
                ./build_frontend.sh
            else
                echo "File build_frontend.sh not found!"
                exit 1  // Fail the build if the file is not found
            fi
            '''
            }
        }
    stage('Build React App') {
        steps {
            dir('frontend') {
                echo 'Installing npm and setting up permissions for build_frontend.sh'
                sh "chmod +x build_frontend.sh"
                sh "./build_frontend.sh"
               }
           }
       }
    }
    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}