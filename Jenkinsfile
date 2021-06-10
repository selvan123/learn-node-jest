pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: "https://github.com/selvan123/learn-node-jest.git"
            }
        }

        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/selvan123/learn-node-jest.git' --branch main

                // Run Maven on a Unix agent.
                sh "npm install"
                sh "npm test"
            }
        }
        
        stage('Static Code Analysis') {
          environment {
            SCANNER_HOME = tool 'SonarQubeScanner'
            ORGANIZATION = "selvans"
            PROJECT_NAME = "selvans_myapp"
          }
          steps {
            withSonarQubeEnv('SonarCloud') {
                sh '''$SCANNER_HOME/bin/sonar-scanner \
                  -Dsonar.projectKey=selvans_myapp \
                  -Dsonar.projectName=myapp \
                  -Dsonar.projectVersion=1.0 \
                  -Dsonar.sources=. \
                  -Dsonar.organization=selvans \
                  -Dsonar.qualitygate.wait=true \
                  -Dsonar.qualitygate.timeout=300 \
                  -Dsonar.sourceEncoding=UTF-8         
            }
          }
        }
    }
}
