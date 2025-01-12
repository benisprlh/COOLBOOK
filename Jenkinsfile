pipeline {
    agent any

    environment {
        // Variabel environment global, misalnya lokasi Java atau Node.js
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-17" 
        PATH = "${env.PATH};${JAVA_HOME}\\bin"
    }

    stages {
        stage('Preparation') {
            steps {
                echo 'Memulai pipeline...'
                // Periksa environment untuk memastikan Jenkins berjalan di Windows
                script {
                    if (!isUnix()) {
                        echo 'Pipeline berjalan di Windows'
                    } else {
                        error 'Pipeline ini dirancang untuk OS Windows!'
                    }
                }
            }
        }

        stage('Checkout Code') {
            steps {
                echo 'Melakukan checkout kode dari repository Git...'
            }
        }

        stage('Build') {
            steps {
                echo 'Build aplikasi...'
                // Contoh menjalankan perintah Windows batch untuk build
                // bat '''
                // echo Build dimulai...
                // mvn clean install
                // echo Build selesai.
                // '''
            }
        }

        stage('Test') {
            steps {
                echo 'Menjalankan pengujian...'
                // Contoh menjalankan pengujian
                // bat '''
                // echo Menjalankan pengujian unit...
                // mvn test
                // echo Pengujian selesai.
                // '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Mendeploy aplikasi...'
                // Simulasi deployment (sesuaikan dengan kebutuhan Anda)
                // bat '''
                // echo Deploying ke server lokal...
                // mkdir C:\\deploy\\app
                // copy target\\*.jar C:\\deploy\\app
                // echo Deployment selesai.
                // '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline selesai!'
        }
        success {
            echo 'Pipeline berhasil dieksekusi!'
        }
        failure {
            echo 'Pipeline gagal!'
        }
    }
}
