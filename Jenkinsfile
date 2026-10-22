pipeline {
    agent any

    parameters {
        string(name: 'NOMBRE', defaultValue: 'Mundo', description: 'A quién saludar')
        choice(name: 'AMBIENTE', choices: ['dev', 'qa', 'prod'], description: 'Ambiente destino')
        booleanParam(name: 'MOSTRAR_INFO', defaultValue: true, description: 'Mostrar info del build')
    }

    environment {
        APP_NAME = 'mi-app'
        VERSION  = "1.0.${BUILD_NUMBER}"
    }

    stages {
        stage('Saludo') {
            steps {
                echo "Hola ${params.NOMBRE}, bienvenido a ${APP_NAME} v${VERSION}"
            }
        }

        stage('Ambiente') {
            steps {
                echo "Desplegando en: ${params.AMBIENTE}"
            }
        }

        stage('Info del build') {
            when {
                expression { params.MOSTRAR_INFO }
            }
            steps {
                sh 'echo "Job: $JOB_NAME | Build: $BUILD_NUMBER"'
            }
        }

        stage('Solo producción') {
            when {
                expression { params.AMBIENTE == 'prod' }
            }
            steps {
                echo '⚠️ Esta etapa solo corre en prod'
            }
        }
    }
}
