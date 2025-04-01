pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'feature/debugging_consoleLog', url: 'https://github.com/munoz138255/Testing-React-Redux-with-Jest-and-Enzyme'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install' // Ajusta según tu stack
            }
        }

        stage('Testing') {
            steps {
                sh 'npm test' // Ejecuta los tests
            }
        }
    }

    post {
        success {
            echo 'Build y testing completados con éxito.'
        }
        failure {
            echo 'Error en la build o tests.'
        }
    }
}
