pipeline{

	agent {label 'linuxslave1'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/vyshnavlal/Push-docker-image-to-Docker-Hub-using-Jenkins-Pipeline.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t vyshnavlal/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push vyshnavlal/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
