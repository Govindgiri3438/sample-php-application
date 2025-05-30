pipeline {
    agent any

    environment {
        DEPLOY_USER = 'ubuntu' // or another SSH user
        DEPLOY_HOST = '3.6.36.20'
        DEPLOY_PATH = '/var/www/html/'
        SSH_CREDENTIALS_ID = 'my-jenkins-ssh'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Govindgiri3438/sample-php-application.git', branch: 'main', credentialsId: 'GIT_CREAD'

            }
        }
        

        stage('Deploy') {
			steps {
				echo 'Starting deployment...'
				sshagent (credentials: ['my-jenkins-ssh']) {
				sh '''
				whoami
				hostname
				echo "Trying SSH..."
				ssh -o StrictHostKeyChecking=no ubuntu@3.6.36.20 "echo Connected"
				'''
        }
    }
}

    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
