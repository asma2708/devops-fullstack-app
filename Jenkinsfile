pipeline {
    agent any

    environment {
        // Define environment variables for your Docker image
//        DOCKER_IMAGE_NAME = 'my-docker-image'
//        DOCKERFILE_PATH = 'Dockerfile' // Path to your Dockerfile
        GITHUB_REPO_URL = 'https://github.com/asma2708/devops-fullstack-app.git' // Replace with your GitHub repo URL
        CREDENTIALS_ID = 'asma git' // Jenkins credentials ID for GitHub (configured in Jenkins)
    }

    stages {
        stage('Checkout Code from GitHub') {
            steps {
                script {
                    // Use Jenkins credentials to clone the GitHub repository
                    checkout([$class: 'GitSCM', 
                              branches: [[name: 'main']], 
                              doGenerateSubmoduleConfigurations: false, 
                              extensions: [[$class: 'CloneOption', depth: 1, noTags: false, reference: '', shallow: true]], 
                              userRemoteConfigs: [[url: GITHUB_REPO_URL, credentialsId: CREDENTIALS_ID]]])
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    //def dockerImage = docker.build("${DOCKER_IMAGE_NAME}:latest", "-f ${DOCKERFILE_PATH} .")
		    echo "In build stage"
                    // Optionally, you can push the Docker image to a registry here
                    // docker.withRegistry('https://your-docker-registry.com', 'your-registry-credentials-id') {
                    //     dockerImage.push()
                    // }
                }
            }
        }
    }

    post {
        success {
            echo 'Build and Docker image creation successful!'
        }
        failure {
            echo 'Build or Docker image creation failed!'
        }
    }
}

