pipeline {
    agent any
    
    stages {
        stage('Restore Packages') {
            steps {
                script {
                    // Define the path to nuget.exe
                    def nugetPath = "C:\\Program Files\\NuGet\\nuget.exe"
                    
                    // Check if nuget.exe exists
                    if (new File(nugetPath).exists()) {
                        // Execute NuGet restore command
                        bat "\"${nugetPath}\" restore \"C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins -declarativePipeline\\WebApplication1.sln\""
                    } else {
                        error "NuGet executable not found at path: ${nugetPath}"
                    }
                }
            }
        }
        
        // Add other stages as needed
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
