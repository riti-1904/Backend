pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SonarQube-Token-1')
    }

    tools {
        nodejs "sonarnode"  // This refers to the NodeJS installation name configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token-1', branch: 'main', url: 'https://github.com/riti-1904/Backend.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'

                    // Install global npm packages
                    bat 'npm install -g eslint@7.32.0'  // Example: Install a specific version of eslint globally
                    bat 'npm install -g nodemon'        // Example: Install nodemon globally
                    bat 'npm install -g typescript'     // Example: Install typescript globally

                    // Install local project dependencies
                    bat 'npm install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    echo 'Starting SonarQube analysis...'
                    bat "sonar-scanner -X -Dsonar.projectKey=your_project_key -Dsonar.sources=src -Dsonar.host.url=http://localhost:9000/dashboard?id=Backe -Dsonar.login=${env.SONAR_TOKEN}"

                    // Replace the Maven command with SonarQube scanner for npm
                    //bat "sonar-scanner -Dsonar.projectKey=your_project_key -Dsonar.sources=src -Dsonar.host.url=http://your-sonarqube-server -Dsonar.login=${env.SONAR_TOKEN}"
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
