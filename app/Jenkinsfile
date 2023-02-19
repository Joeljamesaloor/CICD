pipeline {
    agent any

    environment {
        // Set up your BrowserStack credentials as environment variables
        BROWSERSTACK_USERNAME = credentials('joeljames_BmDiRh')
        BROWSERSTACK_ACCESS_KEY = credentials('ixhhRAs83cMXpxzCbLAJ')
    }

    stages {
        stage('Build') {
            steps {
                // Clone your Git repository
                git url: 'https://github.com/Joeljamesaloor/CICD.git'

                // Build your app (replace this with your own build command)
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy to BrowserStack') {
            steps {
                // Upload your app to BrowserStack
                withCredentials([usernamePassword(credentialsId: 'browserstack-auth', usernameVariable: 'BROWSERSTACK_USERNAME', passwordVariable: 'BROWSERSTACK_ACCESS_KEY')]) {
                    sh 'curl -u $BROWSERSTACK_USERNAME:$BROWSERSTACK_ACCESS_KEY -X POST "https://api-cloud.browserstack.com/app-automate/upload" -F "file=@path/to/your/app"'
                }

                // Start a BrowserStack test session (replace this with your own test command)
                withCredentials([usernamePassword(credentialsId: 'browserstack-auth', usernameVariable: 'BROWSERSTACK_USERNAME', passwordVariable: 'BROWSERSTACK_ACCESS_KEY')]) {
                    sh 'curl -u $BROWSERSTACK_USERNAME:$BROWSERSTACK_ACCESS_KEY -X POST "https://api-cloud.browserstack.com/app-automate/build" -d \'{"app": "bs://<app-id>","devices": ["Samsung Galaxy S8-7.0"],"name": "Jenkins Build"}\' -H "Content-Type: application/json"'
                }
            }
        }
    }
}
