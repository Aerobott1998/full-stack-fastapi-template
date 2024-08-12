pipeline {
    agent any

    environment {
        // Define environment variables, such as database URL, credentials, etc.
        DATABASE_URL = 'postgresql://user:password@localhost:5432/mydatabase'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git 'https://your-repo-url.git'
            }
        }
        
        stage('Install Dependencies') {
            parallel {
                stage('Backend Dependencies') {
                    steps {
                        // Install Python dependencies for FastAPI
                        script {
                            sh 'pip install -r backend/requirements.txt'
                        }
                    }
                }
                stage('Frontend Dependencies') {
                    steps {
                        // Install Node.js dependencies for React
                        script {
                            sh 'cd frontend && npm install'
                        }
                    }
                }
            }
        }
        
        stage('Run Backend Tests') {
            steps {
                // Run pytest for FastAPI tests
                script {
                    sh 'pytest backend/tests'
                }
            }
        }
        
        stage('Build Frontend') {
            steps {
                // Build React frontend
                script {
                    sh 'cd frontend && npm run build'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy scripts, e.g., deploy to a server or cloud service
                script {
                    // Example: Deploy FastAPI app and React app
                    sh 'cd backend && ./deploy.sh'
                    sh 'cd frontend && ./deploy.sh'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
