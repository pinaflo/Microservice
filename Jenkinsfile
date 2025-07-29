pipeline {
    agent any

    stages {
        stage('deploy to kubernetes') {
            steps {
             withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://9B8DF177C701E636018023E5AC8FF339.sk1.eu-west-2.eks.amazonaws.com']]) {
                   sh "kubectl apply -f deployment-service.yml"
                   sleep 60
                }
            }
        }
        
        stage('verify deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://9B8DF177C701E636018023E5AC8FF339.sk1.eu-west-2.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }    
}
