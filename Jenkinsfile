pipeline {
    agent none

    stages {
        // stage('C#') {
        //     agent {
        //         docker { image 'mcr.microsoft.com/dotnet/core/sdk' }
        //     }
        //     steps {
        //         sh 'dotnet build'
        //         sh 'dotnet test'
        //     }
        // }
        stage('Typescript') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web'
                sh 'npm install'
                sh 'npm run build'
                sh 'npm run lint'
                sh 'npm t'
            }
        }
    }
}