pipeline {
    agent any

    stages {
        stage('deploy the app') {
            steps {
                   sh"""
                    docker login -u ${myuser} -p ${mypass}
                    kubectl apply -f app-namespace.yaml
                    kubectl apply -f app-deploy.yaml
                    kubectl apply -f app-service.yaml
                   """
            }
        }
    }
}
