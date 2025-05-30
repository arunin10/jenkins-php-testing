pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/arunin10/jenkins-php-testing.git'
        BRANCH = 'master'
        DEPLOY_DIR = 'D:\\Web\\arul'
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Deploy Files') {
            steps {
                bat """
                echo Cleaning target directory...
                if exist "${DEPLOY_DIR}" rd /s /q "${DEPLOY_DIR}"
                mkdir "${DEPLOY_DIR}"

                echo Copying files to deployment directory...
                xcopy /E /Y "%WORKSPACE%\\*" "${DEPLOY_DIR}\\"
                echo Deployment complete.
                """
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
