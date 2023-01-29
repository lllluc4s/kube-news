pipeline{
    agent any

    stages{
        stage('Build'){
            steps{
                echo 'Building...'
                script{
                    dockerapp = docker.build(
                        "r0drigu3s/kube-news:${env.BUILD_ID}", "-f ./src/Dockerfile ./src"
                        )
                }
            }
        }
        stage('Test'){
            steps{
                echo 'Testing...'
            }
        }
        stage('Deploy'){
            steps{
                echo 'Deploying...'
            }
        }
    }
}