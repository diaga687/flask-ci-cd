pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                git url: 'https://github.com/diaga687/flask-ci-cd.git', branch: 'main'
            }
        }

        stage('Créer un environnement virtuel') {
            steps {
                sh 'python3 -m venv venv'
            }
        }

        stage('Installer les dépendances') {
            steps {
                sh '''
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lancer les tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest
                '''
            }
        }

        stage('Construire l\'image Docker') {
            steps {
                sh 'docker build -t flask-app-ci .'
            }
        }
    }

    post {
        success {
            echo '✅ Tests OK !'
        }
        failure {
            echo '❌ Échec du pipeline'
        }
    }
}
