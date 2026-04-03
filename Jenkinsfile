pipeline {
    agent any

    environment {
        EMAIL = "qanatabbas14@gmail.com"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Qanat-Abbas/repo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                echo "Installing dependencies..."
                pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                echo "Running app..."
                python3 app.py
                '''
            }
        }
    }

    post {
        success {
            emailext (
                subject: "SUCCESS: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build Successful ✅",
                to: "${EMAIL}"
            )
        }

        failure {
            emailext (
                subject: "FAILED: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build Failed ❌",
                to: "${EMAIL}"
            )
        }
    }
}
