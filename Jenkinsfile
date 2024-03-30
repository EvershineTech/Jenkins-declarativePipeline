pipeline {
    agent any

    stages {
        stage('Deploy Project') {
            steps {
                script {
                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace
                    
                    // Define the destination directory
                    def destinationDirectory = "E:/newfolder"

                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Copy files from source to destination
                    bat "xcopy /E /Y \"${sourceDirectory}\" \"${destinationDirectory}\""
                }
            }
        }
    }
}
