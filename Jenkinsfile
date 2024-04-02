pipeline {
    agent any

    stages {
        stage('Build Project') {
            steps {
                script {

                    Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace
                    
                     // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Use MSBuild to build all files in the repository
                    bat "\"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\MSBuild.exe\" \sourceDirectory\" /p:Configuration=Release /t:Rebuild"
                }
            }
        }
        // Add deployment and other stages as needed
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
