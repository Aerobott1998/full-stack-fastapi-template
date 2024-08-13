pipeline {
    agent any

    environment {
        // Define environment variables, such as database URL, credentials, etc.
        DATABASE_URL = 'postgres://postgres:1234@localhost:5432/test_robotics_platform'
    }

    stage('Checkout') {
    steps {
        // Checkout the code from the repository with specified branch and credentials
        git branch: 'dev',
            url: 'https://github.com/Aerobott1998/full-stack-fastapi-template.git',
            credentialsId: 'demo'
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
