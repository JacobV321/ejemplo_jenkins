pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                // Copia todos los archivos al servidor web
                sh 'cp -r * /ruta/de/tu/servidor/web'
            }
        }
    }

    post {
        always {
            // Puedes agregar pasos aquí que se ejecutarán siempre, como limpiar recursos temporales
        }
    }
}
