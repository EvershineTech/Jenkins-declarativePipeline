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

                    def directoryPath = "C:/inetpub/wwwroot/newfolder"
                    if (fileExists(directoryPath)) {
                        // Delete the contents of the directory
                        bat "rmdir /S /Q ${directoryPath}"
                    }
                    // Create the directory
                    bat "mkdir ${directoryPath}"

                    // Copy files from source to destination
                    bat "xcopy /E /Y \"${sourceDirectory}\" \"${destinationDirectory}\""
                }
            }
        }
    }
}
