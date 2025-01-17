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
		    dir('/var/lib/jenkins/workspace/DockerTest/backend'){
		    echo "In build stage"
		    sh "pwd"
		    sh 'ls -la'
		    echo 'ls -la after chown'
		    sh 'sudo chown -R jenkins:jenkins pg_data'
		    sh 'sudo chmod -R 777 pg_data'
		    sh 'sudo chown -R jenkins:jenkins pg_data_test'
		    sh 'sudo chmod -R 777 pg_data_test'
		    echo 'ls -la after chown'
		    sh 'ls -la'
		    sh 'pwd'
		    sh 'sudo docker-compose build'
		    sh 'sudo docker-compose up -d'
		   }
		   
	 	   dir('/var/lib/jenkins/workspace/DockerTest/frontend'){
		   sh 'ls -la'
		   sh "docker build -t my-react-app . "
                   sh "docker run -d -p 3000:3000 my-react-app"
		}  	 	  

	
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

