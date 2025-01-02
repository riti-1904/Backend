pipeline {
    agent any

    environment {
        SONARQUBE = 'http://localhost:9000' // Set your SonarQube URL here
        SONAR_TOKEN = credentials('SONAR_TOKEN') // Use a valid SonarQube token
    }

    tools {
        // Define your tools here (e.g., Git, Maven)
        git 'C:\\Program Files\\Git\\bin\\git.exe' // Ensure this path is correct for Git
        // Maven is optional if you use Maven for building the project
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Use bat for Windows-based commands
                bat 'npm install'  // Replace with your install command, e.g., npm install or mvn install
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Ensure SonarQube Scanner is set up correctly
                    def scannerHome = tool 'SonarQubeScanner' // Ensure the SonarQube Scanner tool is configured
                    withSonarQubeEnv('SonarQube') {
                        bat "${scannerHome}\\bin\\sonar-scanner.bat -Dsonar.projectKey=BackEnd -Dsonar.sources=. -Dsonar.host.url=${env.SONARQUBE} -Dsonar.token=${env.SONAR_TOKEN}"
                    }
                }
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Build or SonarQube analysis completed.'
            }
        }
    }

    post {
        failure {
            echo 'Build or SonarQube analysis failed.'
        }
    }
}
