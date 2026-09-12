pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/danarose22/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
    steps {
        sh '''
            echo "PATH=$PATH"
            which node || true
            which npm || true
            node --version || true
            npm --version || true
        '''
    }
}

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
    }
}
