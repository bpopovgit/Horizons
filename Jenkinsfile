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
                        url: 'https://github.com/bpopovgit/Horizons.git',
                        credentialsId: 'github-credentials'
                    ]]
                ])
            }
        }

        stage('Setup .NET') {
            steps {
                script {
                    def dotnetVersion = bat(script: 'dotnet --version', returnStdout: true).trim()
                    echo "Using .NET Version: ${dotnetVersion}"
                }
            }
        }

        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --configuration Release --no-restore'
            }
        }

        stage('Run Unit & Integration Tests') {
            steps {
                bat 'dotnet test --configuration Release'
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
