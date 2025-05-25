pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials("dhub")
    }
    agent {
        label 'K-M'
    }
    stages {
        stage('git') {
            steps {
                git url:'https://github.com/Saloni2712/Website-PRT-ORG', branch: main
            }
        }
        stage('Docker') {
            steps {
                sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -P ${DOCKERHUB_CREDENTIALS_PSW}'
                sh 'sudo docker build /home/ubuntu/jenkins/workspace/Test-PRT-pipeline/ -t saloni2712/prt-task'
                sh 'sudo docker push saloni2712/prt-task'
            }
        }
        stage('K8s') {
            steps {
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
