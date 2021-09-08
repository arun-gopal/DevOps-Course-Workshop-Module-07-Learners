pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    stages {
        stage('Example') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}