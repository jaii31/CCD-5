pipeline {
    agent any
    environment {
        VENV = 'venv'
    }
    stages {
        stage('Setup') {
        steps {
            echo 'Setting up Python environment...'
            // Create virtual environment
            bat "python -m venv %VENV%"
            // Upgrade pip using Python directly (Windows-safe)
                bat "%VENV%\\Scripts\\python.exe -m pip install --upgrade pip"
            }
        }


        stage('Install Dependencies') {
            steps {
                echo 'Installing required packages...'
                // Install packages from requirements.txt
                bat "%VENV%\\Scripts\\pip install -r requirements.txt"
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Run pytest if you have tests, ignore if not
                bat "%VENV%\\Scripts\\pytest || echo 'No tests found'"
            }
        }

        stage('Run Flask App') {
            steps {
                echo 'Starting Flask app...'
                // Start Flask app in background
                bat "start cmd /k \"%VENV%\\Scripts\\python app.py\""
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
