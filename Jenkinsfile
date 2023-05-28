pipeline {
    agent any

    stages {
        stage('deploy the app') {
            steps {
                   sh"""
                    kubectl apply -f app-namespace.yaml
                    kubectl apply -f app-deploy.yaml
                    kubectl apply -f app-service.yaml
                   """
            }
        }
    }
}
