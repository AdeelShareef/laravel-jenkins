pipeline {
    agent any

    environment {
        APP_KEY = credentials('laravel-app-key')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AdeelShareef/laravel-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t laravel-jenkins .'
            }
        }

        stage('Deploy Laravel') {
            steps {
                sh '''
                    docker rm -f laravel-app || true
                    docker compose up -d --build
                '''
            }
        }

        stage('Verify Endpoint') {
            steps {
                sh 'sleep 5'
                sh 'curl --fail http://localhost:8000'
            }
        }
    }
}
