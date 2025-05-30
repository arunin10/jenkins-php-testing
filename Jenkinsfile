environment {
    staging_server = '10.0.2.12'
    staging_user = 'arul.kumar' // Windows user you created
}

stage('Deploy to Remote') {
    steps {
        powershell '''
        $files = Get-ChildItem -Path "$env:WORKSPACE" -Recurse -File
        foreach ($file in $files) {
            $relativePath = $file.FullName.Substring($env:WORKSPACE.Length + 1)
            $remotePath = "D:/Web/arul/" + $relativePath.Replace("\\", "/")
            $remoteDir = [System.IO.Path]::GetDirectoryName($remotePath)

            ssh $env:staging_user@$env:staging_server "powershell -Command \\"New-Item -ItemType Directory -Force -Path '$remoteDir'\\""
            scp $file.FullName $env:staging_user@$env:staging_server:"$remotePath"
        }
        '''
    }
}
