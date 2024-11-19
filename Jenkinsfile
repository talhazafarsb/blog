pipeline {
    agent any

    stages {
        stage('inall-dependencies') {
            steps {
                echo 'installing dependencies...'
                sh 'cp .env.example .env'
                sh 'composer install'
                sh 'chmod -R 775 storage/'
		        sh 'php artisan config:cache'
		        sh 'php artisan key:gen'
            }
        }
    }
}
