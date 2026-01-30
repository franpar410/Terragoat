pipeline {
    agent any

    environment {
        // Configuramos la ruta de AWS en TerraGoat para el escaneo
        TERRAGOAT_AWS_DIR = "terraform/aws"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Terrascan Scan') {
            steps {
                script {
                    echo "Ejecutando Terrascan en entorno DinD..."
                    // Usamos la imagen oficial de Terrascan
                    // El comando escanea el directorio de AWS y genera un reporte en consola
                    sh "docker run --rm -v \$(pwd):/iac tenable/terrascan scan -t aws -d /iac/${TERRAGOAT_AWS_DIR}"
                }
            }
        }
    }
}
