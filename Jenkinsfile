pipeline {
    agent any

    stages {
        stage('Build Project') {
            steps {
                script {
                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace
                    
                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Specify the path to the project file
                    def projectFile = "${sourceDirectory}/YourProject.csproj" // Replace YourProject.csproj with your actual project file name
                    
                    // Use MSBuild to build the project file
                    bat "\"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\MSBuild.exe\" \"${projectFile}\" /p:Configuration=Release /t:Rebuild"
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
