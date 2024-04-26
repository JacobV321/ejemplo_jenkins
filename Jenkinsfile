pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Este paso clona el repositorio de GitHub en el workspace de Jenkins
                git 'https://github.com/JacobV321/ejemplo_jenkins.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t mi-pagina-web .'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', '542f9ed4-7e83-44ef-af68-fdd88710b056') {
                        def imageName = 'yeicob123/mi-pagina-web:latest'
                        docker.image(imageName).push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Desplegar la imagen Docker (opcional)
                sh 'docker run -d -p 8000:80 yeicob123/mi-pagina-web:latest'
            }
        }
    }
}
