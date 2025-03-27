pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    clusterName: 'EKS-1',
                    credentialsId: 'k8s-token',  // Update with the correct Jenkins credential ID
                    namespace: 'webapps',
                    serverUrl: 'https://3B038E5EC8BBFE74265172A90B7220E6.gr7.us-east-1.eks.amazonaws.com'
                ]]) {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    clusterName: 'EKS-1',
                    credentialsId: 'k8s-token',  // Ensure it matches the new credential
                    namespace: 'webapps',
                    serverUrl: 'https://3B038E5EC8BBFE74265172A90B7220E6.gr7.us-east-1.eks.amazonaws.com'
                ]]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
