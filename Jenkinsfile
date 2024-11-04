pipeline {
    agent any

    environment {
        APP_ENV = 'testing'
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
