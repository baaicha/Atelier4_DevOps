pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "Building the application..."'
                sh 'docker build -t my-python-app .'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                // Ajouter les commandes de tests ici
            }
        }
        stage('Push to Docker Hub') {
            steps {
                sh 'echo "Pushing the Docker image to Docker Hub..."'
                sh 'docker login -u ${DOCKER_HUB_CREDENTIALS_USR} -p ${DOCKER_HUB_CREDENTIALS_PSW}'
                sh 'docker tag my-python-app ${DOCKER_HUB_CREDENTIALS_USR}/my-python-app:latest'
                sh 'docker push ${DOCKER_HUB_CREDENTIALS_USR}/my-python-app:latest'
            }
        }
        stage('Deploy Locally') {
            steps {
                sh 'echo "Deploying the application locally..."'
                sh 'docker stop my-python-app || true'
                sh 'docker rm my-python-app || true'
                sh 'docker run -d -p 5000:5000 --name my-python-app my-python-app'
            }
        }
        stage('Check Credentials') {
           steps {
               echo "Docker Hub user: ${DOCKER_HUB_CREDENTIALS_USR}"
           }
        }

    }
}
