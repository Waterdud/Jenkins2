pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t travel-destination-app:latest .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -d --rm -p 3000:3000 --name travel-test travel-destination-app:latest'
            }
        }
        stage('Test /travel Endpoint') {
            steps {
                script {
                    sleep 3 // Ждём запуск контейнера
                }
                sh 'curl --fail http://localhost:3000/travel'
            }
        }
    }
    post {
        always {
            sh 'docker rm -f travel-test || true'
        }
    }
}
