pipeline {
    agent {
    docker {
        label 'docker'
        image 'python:3.7'
    }
}
    stages {
        stage('Build') {
            steps {
                echo "build"
            }
        }
        stage('Test') {
            steps {
                echo "test"
            }
        }
        stage('Deploy') {
            steps {
                echo "deploy"
            }
        }
    }
}
