pipeline {
    agent any

    environment {
        IMAGE_NAME = "ravi420/ravidocker"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/shankerasdfg-max/branch1.git'
            }
        }

        stage('Install & Test') {
            steps {

                sh 'cd ravi'
                sh 'npm install'
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-creds') {
                        docker.image("${IMAGE_NAME}:${BUILD_NUMBER}").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Simulated deployment stage. Add kubectl apply here if using Kubernetes."
                '''
            }
        }
    }
}
