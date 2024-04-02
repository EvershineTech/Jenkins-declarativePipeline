pipeline {
    agent any
    
    stages {
        stage('Restore Packages') {
            steps {
                bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\nuget.exe" restore "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins -declarativePipeline\\WebApplication1.sln"'
    }
}

    stages {
        stage('Build Project') {
            steps {
                script {
                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])

                    // Define the source directory
                    def sourceDirectory = "${env.WORKSPACE}" // Assuming the repository is cloned into the Jenkins workspace

                    // Use MSBuild to build the project
                   bat "\"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\msbuild.exe\" \"${sourceDirectory}\\WebApplication1.sln\" /p:Configuration=Release /t:Rebuild"

                   // bat "\"C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\MSBuild\\Current\\Bin\\msbuild.exe\" \"${sourceDirectory}\" /p:Configuration=Release /t:Rebuild"
               
                bat '"C:\\Program Files (x86)\\NuGet\\Config\\nuget.exe" restore "${sourceDirectory}\\WebApplication1.sln"'

                }
        
            }
        }

        stage('Restore Packages') {
            steps {
                bat '"C:\\Program Files (x86)\\NuGet\\Config\\nuget.exe" WebApplication1.sln'
            }
        }

        stage('Deploy Project') {
            steps {
                script {
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
        }
    }

    post {
        success {
            script {
                emailext body: 'Deployment successful.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
            }
        }
    }
        failure {
            script {
                emailext body: 'Deployment failed.', subject: 'Project Build Notification', to: 'estsproduct@gmail.com'
            }
        }
    }
}
}
