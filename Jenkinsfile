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
                    withCredentials([usernamePassword(credentialsId: '542f9ed4-7e83-44ef-af68-fdd88710b056', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'docker push yeicob123/mi-pagina-web:latest'
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
