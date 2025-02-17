pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    try {
                        // Clonar el repositorio
                        git url: 'https://github.com/champirongas/my-first-pipeline.git', branch: 'main'
                    } catch (Exception e) {
                        error "Error en el Checkout: ${e.message}"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        // Ejecutar pruebas
                        sh '#!/bin/bash -e\n npm test'
                    } catch (Exception e) {
                        error "Error en Test: ${e.message}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'vercel_token' , variable: 'VERCEL_TOKEN')]) {
                    sh 'vercel --token $VERCEL_TOKEN --prod --yes'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
