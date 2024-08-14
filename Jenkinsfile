pipeline {
    agent {
       docker { image 'alpine:3.20' }
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
