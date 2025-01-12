pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                cd ./app/AndroProject
                npm install
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}