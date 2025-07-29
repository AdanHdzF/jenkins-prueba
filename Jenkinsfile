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
					docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials-not-exists') {
						dockerImage.push(DOCKER_IMAGE_TAG)
					}
				}
			}
			post {
				success {
					echo "Docker image pushed successfully: ${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG}"
				}
				failure {
					script {
						def log = currentBuild.rawBuild.getLog(100).join('\n')

						// echo "Failed to push Docker image: ${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG}"
						mail to: 'adan.hdz.f@gmail.com',
							from: 'adan.hdz.f@gmail.com',
							subject: "Failed to push Docker image: ${env.DOCKER_IMAGE}:${env.DOCKER_IMAGE_TAG}. Job: ${env.JOB_NAME} Build: ${env.BUILD_NUMBER}",
							body: "There was an error pushing the Docker image. Please check the Jenkins job for more details. Job: ${env.JOB_NAME} Build: ${env.BUILD_NUMBER} URL: ${env.BUILD_URL} \n\n ${log}"
					}
					
				}
			}
		}
	}
	
}