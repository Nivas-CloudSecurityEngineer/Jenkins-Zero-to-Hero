# Jenkins Pipeline for Docker Build and Deployment

```groovy
pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Remove existing directory and clone the repository
                sh 'rm -rf devops'
                sh 'git clone https://github.com/nivas-22/devops.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Navigate to the cloned directory and build the Docker image
                sh '''
                    cd devops
                    docker build -t cloud:latest .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run the Docker container with the specified options
                sh 'docker run -itd --name food -p 8081:80 cloud:latest'
            }
        }
    }
}
```
