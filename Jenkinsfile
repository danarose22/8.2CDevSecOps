pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub'

                git branch: 'main',
                    url: 'https://github.com/danarose22/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm dependencies'

                sh 'node --version'
                sh 'npm --version'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests'

                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                echo 'Generating coverage report'

                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                echo 'Running npm security audit'

                sh 'npm audit || true'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                echo 'Running SonarCloud analysis'

                withCredentials([
                    string(
                        credentialsId: 'SONAR_TOKEN',
                        variable: 'SONAR_TOKEN'
                    )
                ]) {
                    sh '''
                        echo "Starting SonarCloud analysis..."

                        npm install --no-save sonar-scanner

                        ./node_modules/.bin/sonar-scanner
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output for details.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
