pipeline{

    agent {label 'linux'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/luanpm1512/vsmon-server.git'
                credentialsId: 'github_login'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t luanpm/vsmon-server:v5'
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push luanpm/vsmon-server:v5'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}