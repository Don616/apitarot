pipeline {
    agent any

    stages{

        stage('Build docker image and Push'){
            steps{
                script{
                    dockerapp = docker.build("don616/apitarot:${env.BUILD_ID}",'-f ./Dockerfile .')
                }
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-don616'){
                        dockerapp.push("${env.BUILD_ID}")
                        dockerapp.push('latest')
                    }
                        
                }
            }
        }
        stage('Deploy Kubernetes'){
            enverionment {
                tag_version = "${env.BUILD_ID}"
            }
            steps{
                withKubeConfig(credentialsId: 'kubeconfig'){
                    sh 'sed -i "s/{{TAG}}/$tagversion/g" .k8s/deployment.yaml'
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }

    }
}