pipeline {
    agent any

    environment {
        // Path ke Node.js (pastikan Node.js sudah diinstal di server Windows)
        NODE_HOME = "C:\\Program Files\\nodejs"
        PATH = "${env.PATH};${NODE_HOME}"
        MONGO_URI=mongodb+srv://benisaprulah5:SB8ypV82i80wOAt4@cluster0.2cocu.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0
        JWT_SECRET="initest"
        REDIS_PASSWORD="nXKEIxZLa4YO1cHWwfc5bnf44wfoUR0S"
        PORT="3000"
        APP_PORT = "3000" // Port React Native App
        SERVER_PORT = "5000" // Port Server
    }

    stages {
        stage('Preparation') {
            steps {
                echo 'Memulai pipeline untuk menjalankan aplikasi React Native di Web...'
                script {
                    if (!isUnix()) {
                        echo 'Pipeline berjalan di Windows'
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
                            start npx expo start --web
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
                            startnpm run dev
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
