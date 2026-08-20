pipeline {
    // 'agent any' tells Jenkins to just use the available workspace, similar to 'runs-on: ubuntu-latest'
    agent any 

    stages {
        stage('1. Checkout Code') {
            steps {
                // This pulls your code from GitHub into the Jenkins workspace
                checkout scm 
            }
        }

        stage('2. Verify File Architecture') {
            steps {
                // Verifying Jenkins can see your specific microservice folders
                sh 'echo "Checking workspace directories..."'
                sh 'ls -la app1_hello/'
                sh 'ls -la tax-app2/'
                sh 'ls -la demo/'
            }
        }

        stage('3. Simulate Docker Build & Push') {
            steps {
                // Note: Running actual Docker commands inside a Jenkins Docker container 
                // requires advanced socket mounting. For this bridge exercise, we echo the logic!
                echo 'Authenticating with Docker Hub...'
                echo 'Building image for app1_hello...'
                echo 'Pushing image to registry...'
            }
        }

        stage('4. Dynamic Tag Injection (sed)') {
            steps {
                // Jenkins uses the 'sh' block to run the exact same Linux commands you used in GitHub
                sh '''
                    echo "Injecting unique build ID into K8s manifests..."
                    # We use Jenkins built-in $BUILD_NUMBER variable instead of github.sha
                    sed -i "s|latest|build-${BUILD_NUMBER}|g" app1_hello/*.yaml
                    cat app1_hello/*.yaml | grep image:
                '''
            }
        }
    }
}