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
                  -Dsonar.projectKey=myapp \
                  -Dsonar.sources=. \
                  -Dsonar.host.url=http://40.71.116.245:9000 \
                  -Dsonar.login=a0433fd7dc16a1fb9cf268e709e9b2dac550a1f2 '''
            }
          }
        }
    }
}
