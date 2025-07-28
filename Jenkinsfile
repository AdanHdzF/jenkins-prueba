pipeline {
	agent any

	environment {
		DOCKER_IMAGE = 'adanhf/echo-test'
		DOCKER_IMAGE_TAG = 'jenkins'
	}

	// triggers {
	// 	pollSCM('H/5 * * * *') // Polls SCM every 5 minutes
	// }

	triggers {
		githubPush() // Trigger on GitHub push events
	}

	stages {
		stage('Checkout') {
			steps {
				git branch: 'main', url: 'https://github.com/AdanHdzF/jenkins-prueba.git'
			}
		}

		stage('Build') {
			steps {
				// bat 'docker build -t adanhf/echo-test:jenkins .'
				script {
					dockerImage = docker.build(DOCKER_IMAGE + ':' + DOCKER_IMAGE_TAG)
				}
			}
		}

		stage('Push') {
			steps {
				script {
					docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
						dockerImage.push(DOCKER_IMAGE_TAG)
					}
				}
			}
		}
	}
	
}