pipeline {
    agent any

    stages {
        stage('Deploy Project') {
            steps {
                script {
                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace
                    
                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Define the destination directory
                    def destinationDirectory = "C:/inetpub/wwwroot/newfolder"
                    
                    // Check if the destination directory already exists
                    if (new File(destinationDirectory).exists()) {
                        
                        // Delete the contents of the directory
                        bat "rmdir /S /Q \"${destinationDirectory}\""
                    }

                    // Create the destination directory
                    bat "mkdir \"${destinationDirectory}\""
                    
                    // Copy files from source to destination
                    bat "xcopy /E /Y \"${sourceDirectory}\" \"${destinationDirectory}\""
                }
            }
            
            post {
                success {
                    emailext subject: "Build Successful",
                              body: "Your build succeeded. Good job!",
                              to: "estsproduct@gmail.com"
                }
                failure {
                    emailext subject: "Build Failed",
                              body: "Your build failed. Please check the logs.",
                              to: "estsproduct@gmail.com"
                }
            }
        }
    }
}
