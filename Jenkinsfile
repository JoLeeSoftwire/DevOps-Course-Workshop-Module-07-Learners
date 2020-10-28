pipeline {
    agent none

    stages {
        stage('C#') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/core/sdk' }
            }
            environment {
                DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
            }
            steps {
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
        stage('Typescript') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web && npm install'
                sh 'cd DotnetTemplate.Web && npm run build'
                sh 'cd DotnetTemplate.Web && npm run lint'
                sh 'cd DotnetTemplate.Web && npm t'
            }
        }
    }
}