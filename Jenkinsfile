pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                git 'https://github.com/diaga687/flask-ci-cd.git'
            }
        }

        stage('Créer un environnement virtuel') {
            steps {
                sh 'python3 -m venv venv'
            }
        }

        stage('Installer les dépendances') {
            steps {
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Lancer les tests') {
            steps {
                sh '. venv/bin/activate && pytest'
            }
        }
    }

    post {
        success {
            echo '✅ Tests OK !'
        }
        failure {
            echo '❌ Erreur dans le pipeline.'
        }
    }
}
