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
            ORGANIZATION = "selvan123-github"
            PROJECT_NAME = "selvan123_myapp"
          }
          steps {
            withSonarQubeEnv('SonarCloud') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                -Dsonar.java.binaries=build/classes/java/ \
                -Dsonar.projectKey=$PROJECT_NAME \
                -Dsonar.sources=.'''
            }
          }
        }
    }
}
