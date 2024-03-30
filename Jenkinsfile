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
                    def remoteDir = '\\\\192.168.1.27\\C$\\inetpub\\wwwroot'
                     def localFiles = 'C:\\inetpub\\wwwroot\\'  // Update this path to your local files
                    
                    // Execute deployment commands using bat
                    bat """
                    mkdir "${remoteDir}"
                    xcopy /s /y "${localFiles}" "${remoteDir}"
                    echo Deployment completed.
                    """
                    }
            }
        }
    }
}
