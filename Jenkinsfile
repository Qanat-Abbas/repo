pipeline {
    agent any

    environment {
        EMAIL = "qanatabbas14@gmail.com"
    }

    stages('Install Dependencies') {
    steps {
        sh '''
        python3 -m venv venv
        . venv/bin/activate
        pip install -r requirements.txt
        '''
    }
      }

    stages('Run Application') {
    steps {
        sh '''
        . venv/bin/activate
        python3 app.py
        '''
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
