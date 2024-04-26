pipeline {
    agent any

    stages {

        stage('Stop and Remove Container') {
            steps {
                script {
                    def containerId = sh(returnStdout: true, script: 'docker ps -aqf "ancestor=yeicob123/mi-pagina-web:latest"').trim()
                    if (containerId) {
                        sh "docker stop $containerId"
                        sh "docker rm $containerId"
                    }
                }
            }
        }

        stage('Preparation') {
            steps {
                script {
                    // Verificar si existe una imagen con el mismo nombre
                    def existingImage = sh(returnStdout: true, script: 'docker images -q mi-pagina-web').trim()
                    if (existingImage) {
                        echo 'Se encontró una imagen existente con el nombre mi-pagina-web. Eliminando la imagen...'
                        sh 'docker rmi mi-pagina-web'
                    } else {
                        echo 'No se encontró una imagen existente con el nombre mi-pagina-web.'
                    }
                }
            }
        }
        
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
                    // Etiquetar la imagen localmente
                    sh 'docker tag mi-pagina-web:latest yeicob123/mi-pagina-web:latest'
        
                    // Iniciar sesión y empujar la imagen a Docker Hub
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
