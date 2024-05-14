pipeline {
    agent any
    
    stages {
        stage('Restore Packages') {
            steps {
                script {
                    // Define the path to nuget.exe ......
                    def nugetPath = "C:/Program Files (x86)/Microsoft Visual Studio/nuget.exe"
                    
                    // Check if nuget.exe exists
                    if (new File(nugetPath).exists()) {
                        // Execute NuGet restore command
                        echo "Restoring NuGet packages..."
                        bat "\"${nugetPath}\" restore \"C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins -declarativePipeline\\WebApplication1.sln\""
                    } else {
                        error "NuGet executable not found at path: ${nugetPath}"
                    }
                }
            }
        }
        
        stage('Build Project') {
            steps {
                script {
                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace

                    // Use MSBuild to build the project
                    echo "Building the project..."
                    bat "\"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\msbuild.exe\" \"${sourceDirectory}\\WebApplication1.sln\" /p:Configuration=Release /t:Rebuild"
                }
            }
        }

        stage('Deploy Project') {
            steps {
                script {
                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace

                    // Define the destination directory
                    def destinationDirectory = "C:/inetpub/wwwroot/newfolder"

                    // Check if the destination directory already exists
                    if (new File(destinationDirectory).exists()) {
                        // Delete the contents of the directory
                        echo "Deleting contents of the destination directory..."
                        bat "rmdir /S /Q \"${destinationDirectory}\""
                    }

                    // Create the destination directory
                    echo "Creating the destination directory..."
                    bat "mkdir \"${destinationDirectory}\""

                    // Copy files from source to destination
                    echo "Copying files from source to destination..."
                    bat "xcopy /E /Y \"${sourceDirectory}\" \"${destinationDirectory}\""
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
