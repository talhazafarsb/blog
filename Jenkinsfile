pipeline {
    agent any

    stages {
        stage('inall-dependencies') {
            steps {
                echo 'installing dependencies...'
                sh 'composer install'
            }
        }
    }
}
