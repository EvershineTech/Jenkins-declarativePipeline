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
                def sourceDirectory = "https://github.com/EvershineTech/Jenkins-declarativePipeline.git"
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
     try {
    copyFiles(new File(sourceDirectory), new File(destinationDirectory))
    println "Project deployed successfully to $destinationDirectory"
} catch (Exception e) {
    println "Error deploying project: $e.message"
}          
                echo 'Deployment completed.'
            }
        }
    }
}


