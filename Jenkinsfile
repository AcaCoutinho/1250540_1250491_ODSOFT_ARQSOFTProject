pipeline {
    agent any  // Run on any available agent/node

    environment {
        APP_NAME = "library-management"
        DEPLOY_ENV = "staging"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building application..."
                sh './gradlew clean build' // or mvn, npm, etc.
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh './gradlew test' // or your test command
            }
            post {
                always {
                    junit '**/build/test-results/test/*.xml'
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying ${APP_NAME} to ${DEPLOY_ENV}..."
                sh './scripts/deploy.sh'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
