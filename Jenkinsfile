pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("travel-destination-app:latest")
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    dockerContainer = dockerImage.run('-d -p 3000:3000')
                }
            }
        }
        stage('Test /travel Endpoint') {
            steps {
                script {
                    sleep 3
                    sh 'curl --fail http://localhost:3000/travel'
                }
            }
        }
    }
    post {
        always {
            script {
                if (dockerContainer) {
                    sh "docker rm -f ${dockerContainer.id}"
                }
            }
        }
    }
}
