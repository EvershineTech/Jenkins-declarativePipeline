pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
              echo "Building the Project.........."
            }
        }
        stage('Test') { 
            steps {
             echo "Testing the Project........"
            }
        }
        stage('Deploy') {
            steps {
               // Create the deployment directory on the local IIS server
                bat "mkdir '\\\\localhost:999\\C$\\inetpub\\wwwroot\\your_application_name'"
                
                // Copy application files to the deployment directory
                bat "xcopy /s /y 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git' '\\\\localhost:999\\C$\\inetpub\\wwwroot\\your_application_name'"
                
                // Print deployment completion message
                echo 'Deployment completed.'
                    }
            }
        }
    }

