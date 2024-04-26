pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Construir la imagen Docker
                script {
                    docker.build('mi-pagina-web')
                }
            }
        }
        stage('Test') {
            steps {
                // Ejecutar pruebas aquí
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // Empujar la imagen a Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', '542f9ed4-7e83-44ef-af68-fdd88710b056') {
                        def imageName = 'yeicob123/mi-pagina-web:latest'
                        docker.image('mi-pagina-web').push(imageName)
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                // Desplegar la imagen en un servidor u otro entorno
                sh 'docker run -d -p 8000:80 tu-usuario/mi-pagina-web:latest'
            }
        }
    }
}
