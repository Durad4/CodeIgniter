pipeline {
    agent any 

    environment {
        CI_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'develop', url: 'https://github.com/Durad4/CodeIgniter.git'
            }
        }

        stage('Install Dependencies') {
            steps {
		sh """
      		rm -rf vendor/ composer.lock
                composer install --no-dev --optimize-autoloader --no-scripts || true
		"""
            }
        }

        stage('Run Tests') {
            steps {
                sh 'phpunit'
            }
            post {
                success {
                    junit 'application/tests/results/*.xml'
                }
                failure {
                    echo 'Tests failed!'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to production environment...'
                // Tambahkan perintah deploy jika ada
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
