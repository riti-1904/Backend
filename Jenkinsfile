pipeline {
    agent any
    tools {
        nodejs 'sonarnode'// Use the NodeJS version configured in Jenkins
    }
    environment {

    SONAR_SCANNER_PATH = 'C:\\Program Files\\sonar-scanner-cli-6.2.1.4610-windows-x64\\sonar-scanner-6.2.1.4610-windows-x64\\bin\\sonar-scanner.bat'

        SONAR_TOKEN = credentials('SonarQube-Token-1') // Use a Jenkins credential for the SonarQube token
    }
    stages {
        stage('Checkout') {
            steps {
                // Pull the code from the GitHub repository
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // Trigger SonarQube analysis
                withSonarQubeEnv('SonarQube-Token-1') { // Replace 'SonarQube' with your SonarQube server name in Jenkins
                    sh 'sonar-scanner -Dsonar.projectKey=Backe \
                                      -Dsonar.sources=. \
                                      -Dsonar.host.url=http://localhost:9000 \
                                      -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }
    }
    post {
        success {
            echo 'Build and SonarQube analysis completed successfully.'
        }
        failure {
            echo 'Build or SonarQube analysis failed.'
        }
    }
}
