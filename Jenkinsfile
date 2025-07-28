pipeline {
	agent any

	environment {
		DOCKER_IMAGE = 'adanhf/echo-test:jenkins'
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
					docker.build(env.DOCKER_IMAGE)
				}
			}
		}
	}
	
}