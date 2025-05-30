pipeline {
    agent any

    environment {
        DEPLOY_USER = 'ubuntu' // or another SSH user
        DEPLOY_HOST = '3.6.36.20'
        DEPLOY_PATH = '/var/www/html/'
        SSH_CREDENTIALS_ID = 'my-jenkins-ssh-id'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'git@github.com:Govindgiri3438/sample-php-application.git', branch: 'main'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'php -l index.php' // simple syntax check, expand as needed
            }
        }

        stage('Deploy') {
            steps {
                sshagent (credentials: [env.SSH_CREDENTIALS_ID]) {
                    sh """
                    ssh -o StrictHostKeyChecking=no $DEPLOY_USER@$DEPLOY_HOST '
                        rm -rf $DEPLOY_PATH/*
                    '
                    scp -r * $DEPLOY_USER@$DEPLOY_HOST:$DEPLOY_PATH
                    """
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
