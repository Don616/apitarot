pipeline {
    agent any

    stages{

        stage('Build docker image'){
            steps{
                script{
                    dockerapp = docker.build("don616/apitarot:${env.BUILD_ID}",'-f ./Dockerfile .')
                }
            }
        }

    }
}