pipeline {
    agent any
    stages {
        stage('Back-end') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0' }
            }
            environment {
                DOTNET_CLI_HOME = '/tmp/DOTNET_CLI_HOME'
            }
            steps {
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
        stage('Front-end') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'node --version'
                dir('DotnetTemplate.Web'){
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm run test-with-coverage'
                    sh 'npm run lint'
                }
            }
        }
    }
    post { 
        always { 
            publishCoverage globalThresholds: [[thresholdTarget: 'Package', unhealthyThreshold: 90.0]], adapters: [istanbulCoberturaAdapter('DotnetTemplate.Web/coverage/cobertura-coverage.xml')]
        }
    }
}