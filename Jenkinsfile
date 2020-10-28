pipeline {
    agent none

    stages {
        stage('C#') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/core/sdk' }
            }
            steps {
                dotnet build
                dotnet test
            }
        }
        stage('Typescript') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                cd DotnetTemplate.Web
                npm install
                npm run build
                npm run lint
                npm t
            }
        }
    }
}