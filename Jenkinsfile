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
                    script {
                    // Define deployment directory and files
                     def dir = 'mkdir "\\\\localhost:999\\C$\\inetpub\\wwwroot"'
                     def localFiles = 'C:\\inetpub\\wwwroot\\IISDemo'  // Update this path to your local files
                    
                    // Execute deployment commands using bat
                        
                    bat """
                     def remoteDir = '\\\\localhost:999\\C$\\inetpub\\wwwroot' // Define the remote directory path
                        mkdir(remoteDir) // Create the directory on the remote server
                    def copyCommand = 'xcopy /s /y "C:\\inetpub\\wwwroot\\IISDemo" "\\\\localhost:999\\C$\\inetpub\\wwwroot"'
                    echo Deployment completed.
                    """
                    }
            }
        }
    }
}
