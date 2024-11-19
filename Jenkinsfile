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
        stage ('creating-containers') {
            steps {
                sh 'docker-compose down -v --rmi all'
                sh 'docker system prune -f'
                echo 'Container creating ...'
                sh 'docker-compose build'
                sh('docker-compose up -d')
                echo 'Containers created successfully'
            }
        }
        
    }
}
