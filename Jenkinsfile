pipeline {
    agent any

    environment {
        staging_server = '10.0.2.12' // replace with your actual server IP or domain
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Remote') {
            steps {
                powershell '''
                # Define local and remote paths
                $localPath = "$env:WORKSPACE\\*"
                $remotePath = "/cygdrive/d/Web/arul/"  # Cygwin path style for SCP compatibility

                # Create remote base directory
                ssh root@${env:staging_server} "mkdir -p /cygdrive/d/Web/arul"

                # Copy entire workspace
                scp -r $localPath root@${env:staging_server}:"$remotePath"
                '''
            }
        }
    }
}
