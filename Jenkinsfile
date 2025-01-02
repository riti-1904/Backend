pipeline {
    agent any

    tools {
        // Ensure NodeJS is set in the Global Tool Configuration
        nodejs 'sonarnode'  // Reference the name of the NodeJS tool you set in Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('SonarQube-Token-1')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/riti-1904/Backend'
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
