pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SonarQube-Token-1')
    }

    stages {
        stage('Checkout') {
            steps {
                // Explicitly mention the branch and credentials for the Git checkout
                git credentialsId: 'github-token-1', branch: 'main', url: 'https://github.com/riti-1904/Backend.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure npm is available and install dependencies using bat
                    echo 'Installing dependencies...'
                    bat 'npm install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    echo 'Starting SonarQube analysis...'
                    bat "mvn sonar:sonar -Dsonar.login=${env.SONAR_TOKEN}"
                }
            }
        }

        stage('Post Actions') {
            steps {
                script {
                    echo 'Build or SonarQube analysis completed.'
                }
            }
        }
    }

    post {
        failure {
            echo 'Build or SonarQube analysis failed.'
        }
    }
}
