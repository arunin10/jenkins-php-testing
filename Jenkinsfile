pipeline{
    agent any
    environment{
        staging_server="10.0.2.12"
    }
    stages{
        stage('deploy to remote'){
            steps{
                sh 'scp ${WORKSPACE}/* root@${staging_server}:D:/Web/arul/'
            }
        }
    }
}
