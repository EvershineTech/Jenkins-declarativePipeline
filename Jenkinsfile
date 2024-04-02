pipeline {
    agent any

    stages {
        stage('Build Project') {
            steps {
                script {
                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Use MSBuild to build all files in the repository
                    bat "\"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\MSBuild.exe\" ${env.WORKSPACE} /p:Configuration=Release /t:Rebuild"
                }
            }
        }
        stage('Deploy Project') {
            steps {
                script {
                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}\\bin\\Release"

                    // Define the destination directory
                    def destinationDirectory = "C:\\inetpub\\wwwroot\\newfolder"

                    // Delete the contents of the destination directory if it exists
                    bat "rmdir /S /Q \"${destinationDirectory}\""

                    // Create the destination directory
                    bat "mkdir \"${destinationDirectory}\""

                    // Copy files from source to destination
                    bat "xcopy /E /Y \"${sourceDirectory}\" \"${destinationDirectory}\""
                }
            }
        }
    }

    post {
        success {
            // Send success email notification
            emailext body: 'Deployment successful.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
        }

        failure {
            // Send failure email notification
            emailext body: 'Deployment failed.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
        }
    }
}
