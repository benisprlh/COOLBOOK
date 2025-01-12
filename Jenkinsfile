pipeline {
    agent any

    stages {
        stage('Preparation') {
            steps {
                echo 'Preparing the environment...'
                sh 'node -v' // Cek versi Node.js
                sh 'npm -v' // Cek versi npm
                sh 'npm -v' // Cek versi npm
                sh 'cd ./MobileApp' // Cek versi npm
            }
        }

        stage('Install Dependencies') {
            parallel {
                stage('Frontend Dependencies') {
                    steps {
                        echo 'Installing frontend dependencies...'
                        dir('./app/AndroProject') {
                            sh 'npm install'
                        }
                    }
                }
                stage('Backend Dependencies') {
                    steps {
                        echo 'Installing backend dependencies...'
                        dir('./server') {
                            sh 'npm install'
                        }
                    }
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                echo 'Running frontend (React Native app for web)...'
                dir('./app/AndroProject') {
                    sh '''
                        npm install -g expo-cli
                        npx expo start --web
                    '''
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                echo 'Running backend (Node.js server)...'
                dir('./server') {
                    sh 'npm run dev'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }

        success {
            echo 'Build and run successful!'
        }

        failure {
            echo 'Build or run failed. Please check logs.'
        }
    }
}
