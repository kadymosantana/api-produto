pipeline {
    agent any
    
    stages {
        stage ("Build Image") {
            steps {
                script {
                    // docker.build (image-name with build id as tag, Dockerfile location and build context)
                    dockerapp = docker.build("fabricioveronez/api-produto:${env.BUILD_ID}", "-f ./src/Dockerfile ./src")
                    // return a DockerImage object for "dockerapp" variable value
                }                
            }
        }       
    }
}