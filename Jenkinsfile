pipeline {
    agent any

    stages {
        stage('inall-dependencies') {
            steps {
                echo 'installing dependencies...'
                sh 'composer install'
            }
        }
#	stage('run-migration') {
#		steps {
#			sh 'php artisan migrate --seed'
#		}
#	}
#	stage('creating images') {
#		steps {
#			sh 'docker-compse build'	
#		}
#	}
    }
}
