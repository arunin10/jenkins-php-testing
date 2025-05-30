node {
    stage('Checkout Code') {
        checkout scm
    }

    stage('Deploy to Local Folder') {
        powershell '''
        $source = "$env:WORKSPACE"
        $destination = "D:\\Web\\arul"

        if (-Not (Test-Path $destination)) {
            New-Item -ItemType Directory -Path $destination -Force
        }

        robocopy $source $destination /MIR /XF *.git* /XD .git
        '''
    }
}
