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
                sh 'docker builder prune -f --all'
                echo 'Container creating ...'
                sh 'docker-compose build'
                sh('docker-compose up -d')
                echo 'Containers created successfully'
            }
        }
        stage ('pushing-containers') {
            steps {
                echo 'pushing docker containers'
                sh 'docker images'
                sh 'docker tag blog-app talhazaffar0/blog-app'
                sh 'docker tag blog-app talhazaffar0/blog-nginx'
                sh 'docker tag blog-app talhazaffar0/blog-db'
                sh 'docker push talhazaffar0/blog-app'
                sh 'docker push talhazaffar0/blog-nginx'
                sh 'docker push talhazaffar0/blog-db'
                echo 'Containers pushed successfully'
            }
        }

    }
}
