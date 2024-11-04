pipeline {
    agent any

    environment {
        APP_ENV = 'local'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/talhazafarsb/blog.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'composer install --no-interaction --prefer-dist --optimize-autoloader'
                sh 'cp .env.example .env'
                sh 'php artisan key:generate'
            }
        }
	stage('Set Up Database') {
            steps {
                sh 'php artisan migrate'
                sh 'php artisan db:seed' 
            }
        }
        stage('Run Tests') {
            steps {
                sh 'vendor/bin/phpunit'
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
