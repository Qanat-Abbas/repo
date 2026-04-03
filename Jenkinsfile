pipeline {
    agent any

    environment {
        EMAIL = "qanatabbas14@gmail.com"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh 'nohup . venv/bin/activate && python3 app.py > flask.log 2>&1 &'
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
