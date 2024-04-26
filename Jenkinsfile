pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t mi-pagina-web .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8000:80 mi-pagina-web'
            }
        }
    }
}
