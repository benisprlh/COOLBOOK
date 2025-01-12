pipeline {
    agent any

    environment {
        // Path ke Node.js (pastikan Node.js sudah diinstal di server Windows)
        NODE_HOME = "C:\\Program Files\\nodejs"
        PATH = "${env.PATH};${NODE_HOME}"
    }

    stages {
        stage('Preparation') {
            steps {
                echo 'Memulai pipeline untuk menjalankan aplikasi React Native di Web...'
                script {
                    if (!isUnix()) {
                        echo 'Pipeline berjalan di Windows'
                    } else {
                        error 'Pipeline ini dirancang untuk OS Windows!'
                    }
                }
            }
        }

        stage('Install Dependencies for App') {
            steps {
                echo 'Berpindah ke direktori ./app/AndroProject dan menginstal dependensi aplikasi...'
                dir('./app/AndroProject') {
                    bat '''
                    echo Menginstal dependensi aplikasi...
                    npm install
                    echo Dependensi aplikasi berhasil diinstal.
                    '''
                }
            }
        }

        stage('Install Dependencies for Server') {
            steps {
                echo 'Berpindah ke direktori ./server dan menginstal dependensi server...'
                dir('./server') {
                    bat '''
                    echo Menginstal dependensi server...
                    npm install
                    echo Dependensi server berhasil diinstal.
                    '''
                }
            }
        }

        stage('Run Applications') {
            parallel {
                stage('Run React Native App') {
                    steps {
                        echo 'Menjalankan aplikasi React Native...'
                        dir('./app/AndroProject') {
                            bat '''
                            echo Memulai aplikasi React Native...
                            npx expo start --web
                            '''
                        }
                    }
                }
                stage('Run Server') {
                    steps {
                        echo 'Menjalankan server backend...'
                        dir('./server') {
                            bat '''
                            echo Memulai server backend...
                            npm run dev
                            '''
                        }
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline selesai!'
        }
        success {
            echo 'Pipeline berhasil menjalankan aplikasi dan server!'
        }
        failure {
            echo 'Pipeline gagal! Periksa log untuk detailnya.'
        }
    }
}
