pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0' 
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: 'feature-ci-pipeline']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/YOUR_GITHUB_USERNAME/REPO_NAME.git',
                        credentialsId: 'github-credentials'
                    ]]
                ])
            }
        }

        stage('Setup .NET') {
            steps {
                script {
                    def dotnetVersion = sh(script: 'dotnet --version', returnStdout: true).trim()
                    echo "Using .NET Version: ${dotnetVersion}"
                }
            }
        }

        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --configuration Release --no-restore'
            }
        }

        stage('Run Unit & Integration Tests') {
            steps {
                sh 'dotnet test --configuration Release'
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed."
        }
        success {
            echo "Build and tests completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs for errors."
        }
    }
}
