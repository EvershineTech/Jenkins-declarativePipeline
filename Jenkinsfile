pipeline {
    agent any

    stages {
        stage('Build Project') {
            steps {
                script {
                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Use MSBuild to build the .NET web application
                    bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\MSBuild.exe" "${env.WORKSPACE}/Jenkins-declarativePipeline" /p:Configuration=Release /t:Rebuild'

                    // Check if the build was successful
                    if (currentBuild.result == 'SUCCESS') {
                        // Archive the build files
                        archiveArtifacts artifacts: '**/bin/Release/**', fingerprint: true
                    } else {
                        error('Build failed. Deployment stage will not be executed.')
                    }
                }
            }
        }
        stage('Deploy Project') {
            steps {
                script {
                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}/Jenkins-declarativePipeline"

                    // Define the destination directory
                    def destinationDirectory = "C:\\inetpub\\wwwroot\\newfolder"

                    // Delete the contents of the destination directory if it exists
                    bat "rmdir /S /Q \"${destinationDirectory}\""

                    // Copy files from source to destination
                    bat "xcopy /E /Y \"${sourceDirectory}\\*.*\" \"${destinationDirectory}\""
                }
            }
        }
    }

    post {
        success {
            // Pack all build artifacts into a zip file
            archiveArtifacts artifacts: '**/*', allowEmptyArchive: true, onlyIfSuccessful: true, excludes: 'E:/Build packup/**'
            
            // Send success email notification
            emailext body: 'Deployment successful.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
        }

        failure {
            // Send failure email notification
            emailext body: 'Deployment failed.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
        }
    }
}
