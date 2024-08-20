pipeline {
    agent any

    // Define environment variables if needed
    environment {
        BRANCH_NAME = "${env.BRANCH_NAME}"
    }

    stages {
        stage('Check Branch Conditions') {
            when {
                // Run only for specific branch names and conditions
                expression {
                    def branchName = env.BRANCH_NAME
                    return branchName.startsWith('release') || branchName == 'develop'
                }
            }
            steps {
                script {
                    // Additional logic to determine if the pipeline should run
                    def shouldRun = false

                    // PR to release* branch
                    if (env.CHANGE_ID && env.CHANGE_TARGET.startsWith('release')) {
                        shouldRun = true
                    }

                    // Push to release* branch
                    if (branchName.startsWith('release')) {
                        shouldRun = true
                    }

                    // Merge to release* branch
                    if (branchName.startsWith('release') && env.GIT_COMMIT_MESSAGE.contains('Merge')) {
                        shouldRun = true
                    }

                    // PR to develop branch
                    if (env.CHANGE_ID && env.CHANGE_TARGET == 'develop') {
                        shouldRun = true
                    }

                    if (!shouldRun) {
                        // Skip the build if conditions are not met
                        currentBuild.result = 'SUCCESS'
                        return
                    }

                    echo "Running the pipeline for branch: ${branchName}"
                }
            }
        }

        // Define other stages as needed
        stage('Build') {
            steps {
                echo "Building the project..."
                // Add your build steps here
            }
        }
        
        stage('Test') {
            steps {
                echo "Running tests..."
                // Add your test steps here
            }
        }
        
        stage('Deploy') {
            steps {
                echo "Deploying the application..."
                // Add your deploy steps here
            }
        }
    }

    post {
        always {
            echo "Cleaning up..."
            // Add any cleanup steps here
        }
    }
}
