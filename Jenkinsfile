pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Branch is: ${env.BRANCH_NAME}"
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                script {
                    echo "Running build+test on branch ${env.BRANCH_NAME}"
                    sh 'mvn clean test -q'
                }
            }
        }

        stage('Custom Step') {
            when {
                branch "dev"
            }
            steps {
                echo "This is additional dev-only step"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying artifacts for branch ${env.BRANCH_NAME}"
                // Simulate deployment
                sh "echo Deployed branch ${env.BRANCH_NAME}"
            }
        }
    }

    post {
        success {
            echo "SUCCESS: ${env.BRANCH_NAME}"
        }
        failure {
            echo "FAILURE: ${env.BRANCH_NAME}"
        }
    }
}
