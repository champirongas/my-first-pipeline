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

        stage('Build') {
            steps {
                script {
                    try {
                        // Verificar si npm está instalado
                        sh 'command -v npm || { echo "npm no está instalado"; exit 1; }'
                        // Instalar dependencias
                        sh '#!/bin/bash -e\n npm install'
                    } catch (Exception e) {
                        error "Error en Build: ${e.message}"
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
                script {
                    try {
                        // Lógica de despliegue (por ejemplo, subir a un proveedor de la nube)
                        echo 'Deploying application...'
                    } catch (Exception e) {
                        error "Error en Deploy: ${e.message}"
                    }
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
