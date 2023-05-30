pipeline {
    agent {
        label 'aws-slave'
    }

    stages {
        stage('build and push image to docker hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: 'mypass', usernameVariable: 'myuser')]) {
                   sh"""
                    docker build . -t mahaelkomey/test-web-app:v1.0
                    docker login -u ${myuser} -p ${mypass}
                    docker push mahaelkomey/test-web-app:v1.0
                   """
                }
            }
        }
        
        stage('deploy the app') {
            steps {
                 withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: 'mypass', usernameVariable: 'myuser')]) {
                       sh"""
                        docker login -u ${myuser} -p ${mypass}
                        kubectl delete deployment --all -n jenkins-ns
                        kubectl apply -f app-namespace.yaml
                        kubectl apply -f app-deploy.yaml
                        kubectl apply -f app-service.yaml
                       """
                 }
            }
        }
    }
}
