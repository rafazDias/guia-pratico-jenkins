pipeline{
    agent any

    stages{
        stage('Docker build') {
            steps{
                script{
                    dockerapp = docker.build("rafaelldiass/teste:${env.BUILD_ID}", '-f ./src/Dockerfile ./src' )
                }
            }
        }
            stage('Push Image') {
            steps{
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.push('latest')
                        docker.push("${env.BUILD_ID}")
                    }
                
                }
            }
        }

                stage('Deploy Kubernetes') {
            steps{
                sh 'echo "Executando comando kubectl apply"'
            }
        }
    }
}