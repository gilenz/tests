pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'apk add python3'
                sh 'apk add python3 python3-pip'
                sh 'apk add pip install poetry'
            }
        }

        stage('Determine Version') {
            steps {
                sh 'poetry version patch'
            }
        }

        stage('Tag and Push') {
            steps {
                script {
                    def newVersion = sh(script: "poetry version | cut -d' ' -f2", returnStdout: true).trim()
                    sh "git commit -am 'Bump version to ${newVersion}'"
                    sh 'git push origin HEAD'
                    sh "git tag v${newVersion}"
                    sh 'git push --tags'
                }
            }
        }
    }
}
