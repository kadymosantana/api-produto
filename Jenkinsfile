pipeline {
    agent any
    
    stages {
        stage ("Build Image") {
            steps {
                script {
                    // docker.build (image-name with build id as tag, Dockerfile location and build context)
                    dockerapp = docker.build("kadymo/api-produto:${env.BUILD_ID}", "-f ./src/Dockerfile ./src")
                    // return a DockerImage object for "dockerapp" variable value
                }                
            }
        }

        stage ("Push image") {
            steps {
                script {
                    // Registring the built image with its tags on Dockerhub
                    docker.withRegistry("", "kadymo-dockerhub") {
                        dockerapp.push("latest")
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage ("Deploy Kubernetes") {
            environment {
                tag_version = "${env.BUILD_ID}"
            }
            steps {
                // Setting credentials with the Kubernetes CLI plugin and deploying the manifest file
                withKubeConfig([credentialsId: "kubeconfig"]) {
                    sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/deployment.yaml'
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }
    }
}