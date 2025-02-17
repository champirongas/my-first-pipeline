pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'vercel_token', variable: 'VERCEL_TOKEN')]) {
                    sh 'vercel --token $VERCEL_TOKEN --prod'
                }
            }
        }
    }
}
