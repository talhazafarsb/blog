pipeline {
    agent any

    stages {
        stage('inall-dependencies') {
            steps {
                echo 'installing dependencies...'
		sh 'php artisan config:cache'
		sh 'php artisan key:gen'
                sh 'composer install'
		sh 'php artisan migrate:refresh --seed'
            }
        }
    }
}
