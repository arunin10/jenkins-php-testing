pipeline {
    agent any

    environment {
        staging_server = '10.0.2.12'
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
                    $files = Get-ChildItem -Path "$env:WORKSPACE" -Recurse -File
                    foreach ($file in $files) {
                        $relativePath = $file.FullName.Substring($env:WORKSPACE.Length + 1)
                        $remotePath = "D:/Web/arul/" + $relativePath.Replace("\\", "/")
                        $remoteDir = [System.IO.Path]::GetDirectoryName($remotePath)

                        ssh deployer@${env:staging_server} "mkdir -p `"$remoteDir`""
                        scp $file.FullName deployer@${env:staging_server}:"$remotePath"
                    }
                '''
            }
        }
    }
}
