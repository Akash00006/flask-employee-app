
pipeline {

    agent any

    stages {

        stage('Create Virtual Environment') {
            steps {
                sh '''
                    python3 --version
                    python3 -m venv venv
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Flask Application') {
            steps {
                sh '''
                    . venv/bin/activate
                    python -m py_compile app.py
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
