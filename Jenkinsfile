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
        stage ('logging docker and pushing-containers') {
            steps {
                echo 'Logging into Docker Hub and pushing containers'
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                   sh """
                   echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin

                   docker tag blog-app talhazaffar0/blog-app
                   docker tag blog-db talhazaffar0/blog-db
                   docker tag blog-nginx talhazaffar0/blog-nginx

                   docker push talhazaffar0/blog-app
                   docker push talhazaffar0/blog-db
                   docker push talhazaffar0/blog-nginx
                   """
                }
            }
        }

    }
}
