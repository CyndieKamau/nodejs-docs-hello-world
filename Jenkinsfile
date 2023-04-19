pipeline {
    agent any

    environment {
        AWS_REGION = 'us-west-2'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/CyndieKamau/nodejs-docs-hello-world.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Package') {
            steps {
                sh 'npm run build'
                sh 'tar -czvf nodejs-docs-hello-world.tar.gz hello-world/'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'your-aws-credentials-id', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    sh 'aws s3 cp your-app.tar.gz s3://your-bucket-name
