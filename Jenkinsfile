pipeline {
    agent any
    
    stages {
        stage ("Build Image") {
            steps {
                script {
                    // docker.build (image-name, Dockerfile specification, Dockerfile and build context)
                    dockerapp = docker.build("fabricioveronez/api-produto", "-f ./src/Dockerfile ./src")
                    // return a DockerImage object for "dockerapp" variable value
                }                
            }
        }       
    }
}