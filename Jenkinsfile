pipeline {
    agent any

    tools {
        nodejs 'Node 18'  // Asegúrate de tenerlo configurado en Jenkins: Manage Jenkins > Global Tool Configuration
    }

    triggers {
        githubPush() // <-- Ejecuta el pipeline automáticamente en cada push (requiere webhook)
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
                bat 'set "NODE_OPTIONS=--openssl-legacy-provider" && npm run build' //cambios en nodejs +17
            }
        }

        stage('Lint') {
            steps {
                bat 'npm run lint'    // verificacion de código con herramienta lint
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'          // para ejecutar pruebas unitarias
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true         // ideal para guardar resultados y luego integrar en otras etapas (despliegue por ejemplo)
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
