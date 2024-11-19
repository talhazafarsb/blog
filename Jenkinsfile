pipeline {
    agent any
    environment {
        DB_DATABASE='db_blog'
        DB_PASSWORD='!@bugdeaL3r'
    }
    stages {
        stage('inall-dependencies') {
            steps {
                echo 'installing dependencies...'
                sh 'cp .env.example .env'
                sh 'composer install'
		        sh 'php artisan config:clear'
		        sh 'php artisan key:gen'
                sh 'php artisan config:cache'
            }
        }
        stage('Run-test') {
            steps {
                sh 'php artisan test'
            }
        }
        
    }
}
