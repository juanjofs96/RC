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
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test -- --watchAll=false'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        // Opcional: etapa de despliegue
        // stage('Deploy') {
        //     steps {
        //         sh './deploy.sh'  // Ejemplo, debes definirlo
        //     }
        // }
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
