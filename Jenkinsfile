pipeline {
    agent any

    environment {
        EMAIL = "qanatabbas14@gmail.com"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                python3 app.py
                '''
            }
        }
    }

    post {
        success {
            emailext (
                subject: "SUCCESS: ${env.JOB_NAME}",
                body: "Build Successful ✅",
                to: "${EMAIL}"
            )
        }

        failure {
            emailext (
                subject: "FAILED: ${env.JOB_NAME}",
                body: "Build Failed ❌",
                to: "${EMAIL}"
            )
        }
    }
}
