pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'feature-ci-pipeline', url: 'https://github.com/YOUR_GITHUB_USERNAME/REPO_NAME.git'
            }
        }

        stage('Setup .NET') {
            steps {
                sh 'dotnet --version'
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
                sh 'dotnet test'
            }
        }
    }
}
