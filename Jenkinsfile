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

                    // Change directory to where your project or solution file is located
                    dir("${sourceDirectory}") {
                        // Use msbuild to build your .NET project
                        bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\MSBuild.exe" E:\Build packup /p:Configuration=Release /t:Rebuild'
                    }
                }
            }
        }
        stage('Deploy Project') {
            steps {
                script {
                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace
                    
                    // Define the destination directory
                    def destinationDirectory = "C:\\inetpub\\wwwroot\\newfolder"
                    
                    // Check if the destination directory already exists
                    if (new File(destinationDirectory).exists()) {
                        // Delete the contents of the directory
                        bat "rmdir /S /Q \"${destinationDirectory}\""
                    }

                    // Create the destination directory
                    bat "mkdir \"${destinationDirectory}\""
                    
                    // Copy files from source to destination
                    bat "xcopy /E /Y \"${sourceDirectory}\\*.*\" \"${destinationDirectory}\""
                }
            }
        }
    }

    post {
        success {
            script {
                emailext body: 'Deployment successful.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
            }
        }

        failure {
            script {
                emailext body: 'Deployment failed.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
            }
        }
    }
}
