pipeline{
    agent any

    stages{
        stage('Docker build') {
            steps{
                sh 'echo "Executando comando Docker build"'
            }
        }
            stage('Push Image') {
            steps{
                sh 'echo "Executando comando Docker push"'
            }
        }

                stage('Deploy Kubernetes') {
            steps{
                sh 'echo "Executando comando kubectl apply"'
            }
        }
    }
}