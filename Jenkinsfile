pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t todos-app:latest .'
                }
            }
        }

        stage('Push to Registry') {
            steps {
                script {
                    // Push Docker image to registry
                    withCredentials([usernamePassword(credentialsId: 'docker-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'docker push your-registry/todos-app:latest'
                    }
                }
            }
        }

        stage('Deploy with Helm') {
            steps {
                script {
                    // Deploy with Helm
                    sh 'helm install todos-app ./path/to/todos-chart'
                }
            }
        }
    }
}