pipeline {
    agent any
    environment {
        BROWSER_STACK_USERNAME = 'joeljames_BmDiRh'
        BROWSER_STACK_ACCESS_KEY = 'ixhhRAs83cMXpxzCbLAJ'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], 
                userRemoteConfigs: [[url: 'https://github.com/Joeljamesaloor/CICD.git']]])
            }
        }
        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('Deploy to BrowserStack') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'browserstack-credentials', 
                usernameVariable: 'BROWSER_STACK_USERNAME', passwordVariable: 'BROWSER_STACK_ACCESS_KEY')]) {
                    sh 'npm install -g browserstack-cypress-cli'
                    sh 'browserstack-cypress run --sync --key $BROWSER_STACK_ACCESS_KEY --username $BROWSER_STACK_USERNAME'
                }
            }
        }
    }
}
