pipeline {
    agent any

    environment {
        DEPLOY_DIR = '/home/alumno/Documentos/Usuarios/practica9/Testing-React-Redux-with-Jest-and-Enzyme'  // Ruta donde se encuentra tu proyecto dentro del contenedor
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout del código para la rama actual
                    git branch: env.BRANCH_NAME, url: 'https://github.com/munoz138255/Testing-React-Redux-with-Jest-and-Enzyme/tree/master'
                }
            }
        }

        // Pipeline de CI para la rama feature
        stage('Build') {
            when {
                branch 'feature/*'  // Solo se ejecuta en ramas que empiecen con 'feature/'
            }
            steps {
                script {
                    // Ejecutar comandos de build según el stack que estés usando (ejemplo con npm)
                    echo "Construyendo proyecto en la rama feature"
                    sh 'npm install'
                }
            }
        }

        stage('Testing') {
            when {
                branch 'feature/*'  // Solo se ejecuta en ramas que empiecen con 'feature/'
            }
            steps {
                script {
                    // Ejecutar pruebas
                    echo "Ejecutando pruebas en la rama feature"
                    sh 'npm test'
                }
            }
        }

        // Despliegue en el contenedor, solo si es la rama 'master'
        stage('Deploy') {
            when {
                branch 'master'  // Solo se ejecuta en la rama 'master'
            }
            steps {
                script {
                    // Despliegue en el contenedor, simplemente ejecutando los comandos necesarios en el contenedor
                    echo "Desplegando proyecto en la rama master"
                    sh """
                        cd ${DEPLOY_DIR}
                        git pull origin master  # Traer los últimos cambios
                        npm install  # Instalar dependencias si es necesario
                        npm run build  # Si usas build scripts
                        # Añadir otros pasos de despliegue necesarios
                        echo 'Despliegue completado con éxito dentro del contenedor'
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline ejecutado correctamente.'
        }
        failure {
            echo 'Hubo un error en la ejecución del pipeline.'
        }
    }
}
