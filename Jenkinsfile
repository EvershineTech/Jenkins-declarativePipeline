pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
              echo "Building the Project.........."
            }
        }
        stage('Test') { 
            steps {
             echo "Testing the Project........"
            }
               }
        
        stage('Deploy') {
            steps {
                  checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/EvershineTech/Jenkins-declarativePipeline.git']]])
                def sourceDirectory = "${env.WORKSPACE}"
                def destinationDirectory = "E:/newfolder"
                def copyFiles = { File src, File dest ->
    if (src.isDirectory()) {
        dest.mkdirs()
        src.eachFile { file ->
            copyFiles(file, new File(dest, file.name))
        }
    } else {
        dest.bytes = src.bytes
    }
}
     bat "xcopy /E /Y \"${sourceDirectory}\" \"${destinationDirectory}\""
                echo 'Deployment completed.'
            }
        }
    }
}


