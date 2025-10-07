pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                bat 'gradlew.bat clean build'  // ✅ Windows uses bat
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'gradlew test'  // ✅ Windows uses bat
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
                echo 'Deploying...'
                bat 'scripts\\deploy.bat'  // ✅ or adjust path to your deploy script
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
