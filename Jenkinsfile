pipeline {
	agent any

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
				bat 'echo "Building the project..."'
			}
		}
	}
	
}