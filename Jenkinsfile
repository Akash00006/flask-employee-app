
pipeline {
    agent {
        docker {
            image 'python:3.12'
            args '-u root'
        }
    }

    stages {

        stage('Check Python') {
            steps {
                sh '''
                    python --version
                    pip --version
                '''
            }
        }

        stage('Create Virtual Environment') {
            steps {
                sh '''
                    python -m venv venv
                    ./venv/bin/python --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    ./venv/bin/python -m pip install --upgrade pip
                    ./venv/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Flask Application') {
            steps {
                sh '''
                    ./venv/bin/python -m py_compile app.py
                    echo "Flask application validation successful!"
                '''
            }
        }
    }

    post {
        success {
            echo 'Flask application build successful!'
        }

        failure {
            echo 'Pipeline execution failed!'
        }
    }
}
