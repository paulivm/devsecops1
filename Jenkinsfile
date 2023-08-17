pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('checkout') {
            steps {
                checkout scm
            }
        }

      stage('tfsec') {
            steps {
                script {
                    bat 'docker pull aquasec/tfsec'
                    bat 'docker run --rm -v "${WORKSPACE}:/src" aquasec/tfsec /src'
                    }
                }
            }
        
    stage('Approval for Terraform') {
            steps {
                input(message: 'Approval required before Terraform', ok: 'Proceed', submitterParameter: 'APPROVER')
            }
        }

        stage('terraform') {
            steps {
                bat 'C:\\Documentos\terraform.exe apply -auto-approve -no-color'
                }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
