pipeline{
    agent any

    stages{
        stage('Build Docker Image'){
            steps{
                echo 'Building...'
                script{
                    dockerapp = docker.build(
                        "r0drigu3s/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src'
                        )
                }
            }
        }

        stage('Push Docker Image'){
            steps{
                echo 'Pushing...'
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage ('Deploy Kubernetes'){
            steps{
                echo 'Deploying...'
                script{
                    withKubeConfig([credentialsId: 'kubeconfig']){
                        sh 'kubectl apply -f ./k8s/deployment.yaml'
                    }
                }
            }
        }
    }
}