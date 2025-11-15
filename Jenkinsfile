pipeline {
    agent any

    // Example environment variables (for demo only).
    // We are NOT really installing Chrome in this workshop.
    environment {
        CHROME_VERSION       = 'YOUR_CHROME_VERSION_HERE'
        CHROMEDRIVER_VERSION = 'YOUR_CHROMEDRIVER_VERSION_HERE'
        CHROME_INSTALL_PATH  = 'C:\\Program Files\\Google\\Chrome\\Application'
        CHROMEDRIVER_PATH    = 'C:\\Program Files\\Google\\Chrome\\Application\\chromedriver.exe'
    }

    stages {

        stage('Checkout code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/QA-Automation-Testing-Demo/Selenium_IDE.git'
            }
        }

        stage('Set up .NET Core') {
            steps {
                bat '''
echo Checking .NET SDK installation...
dotnet --info
'''
            }
        }

        stage('Uninstall Current Chrome (demo only)') {
            steps {
                bat '''
echo [INFO] Demo step only – NOT uninstalling Chrome on this machine.
'''
            }
        }

        stage('Install Specific Version of Chrome (demo only)') {
            steps {
                bat '''
echo [INFO] Demo step only – NOT installing Chrome here.
echo Would target Chrome version: %CHROME_VERSION%
'''
            }
        }

        stage('Download and Install ChromeDriver (demo only)) {
            steps {
                bat '''
echo [INFO] Demo step only – NOT downloading ChromeDriver.
echo Would target ChromeDriver version: %CHROMEDRIVER_VERSION%
echo Expected ChromeDriver path: %CHROMEDRIVER_PATH%
'''
            }
        }

        stage('Restore dependencies') {
            steps {
                bat '''
echo Restoring project dependencies...
dotnet restore SeleniumIde.sln
'''
            }
        }

        stage('Build') {
            steps {
                bat '''
echo Building solution...
dotnet build SeleniumIde.sln --configuration Release
'''
            }
        }

        stage('Run tests') {
            steps {
                bat '''
echo Running tests...
dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"
'''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            junit '**/TestResults/*.trx'
        }
    }
}
