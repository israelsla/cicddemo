pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the latest code from the repository
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image for the Flask app
                sh 'docker build -t flask-jenkins-demo .'
            }
        }

        stage('Deploy App') {
            steps {
                // Stop any existing container
                sh 'docker stop flask-container || true && docker rm flask-container || true'
                
                // Run the Flask app in a new container
                sh 'docker run -d --name flask-container -p 5001:5000 flask-jenkins-demo'
            }
        }
    }

    post {
        success {
            echo "Application deployed successfully!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}

