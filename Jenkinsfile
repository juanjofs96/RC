pipeline {
    agent any

    tools {
        nodejs 'Node 18'  // Asegúrate de tenerlo configurado en Jenkins: Manage Jenkins > Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ahfarmer/calculator.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                bat 'npm run deploy'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizado'
        }
        success {
            echo '¡Todo pasó correctamente!'
        }
        failure {
            echo 'Falló alguna etapa del pipeline'
        }
    }
}
