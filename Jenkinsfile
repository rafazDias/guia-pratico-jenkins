pipeline{
    agent any
    post {
        always {
            // Chuck Norris aparece em todos os builds
            chuckNorris()
        }
       
        success {
            echo '🚀 Deploy realizado com sucesso!'
            echo '💪 Chuck Norris aprova seu pipeline DevSecOps!'
            echo "✅ Imagem jamalshadowdev/meuapp:${env.BUILD_ID} deployada no Kubernetes"
        }
       
        failure {
            echo '❌ Build falhou, mas Chuck Norris nunca desiste!'
            echo '🔍 Chuck Norris está investigando o problema...'
            echo '💡 Verifique: Docker build, DockerHub push ou Kubernetes deploy'
        }
       
        unstable {
            echo '⚠️ Build instável - Chuck Norris está monitorando'
        }
    }
    stages{
        stage('Docker build') {
            steps{
                script{
                    dockerapp = docker.build("rafaelldiass/pipeguiajenkins:${env.BUILD_ID}", '--no-cache -f ./src/Dockerfile ./src' )
                }
            }
        }
            stage('Push Image') {
            steps{
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                
                }
            }
        }

                stage('Deploy Kubernetes') {
                    environment {
                        tag_version =  "${env.BUILD_ID}"
                    }
            steps{
                withKubeConfig([credentialsId: 'kubeconfig']){
                    sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/deployment.yaml'
                    sh "kubectl apply -f k8s/deployment.yaml"
                }
                
            }
        }
    }
}