pipeline {
    agent any

    // Example environment variables (demo only, not actually used for installs)
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
echo [INFO] Demo step only - NOT uninstalling Chrome on this machine.
'''
            }
        }

        stage('Install Specific Version of Chrome (demo only)') {
            steps {
                bat '''
echo [INFO] Demo step only - NOT installing Chrome here.
echo Would target Chrome version: %CHROME_VERSION%
'''
            }
        }

        stage('Download and Install ChromeDriver (demo only)') {
            steps {
                bat '''
echo [INFO] Demo step only - NOT downloading ChromeDriver.
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
            // Keep all test result files as build artifacts
            archiveArtifacts artifacts: '**/TestResults/*.*', allowEmptyArchive: true

            // Note for students:
            // JUnit plugin expects JUnit-style XML, not .trx.
            // In a real project we would convert TRX to JUnit XML
            // or use a compatible logger, then call 'junit' here.
        }
    }
}
