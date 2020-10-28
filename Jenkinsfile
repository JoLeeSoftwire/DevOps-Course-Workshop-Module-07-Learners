pipeline {
    agent none

    stages {
        stage('C#') {
            agent {
                // docker { image 'mcr.microsoft.com/dotnet/core/sdk' }
                docker { image 'node:14-alpine' }
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