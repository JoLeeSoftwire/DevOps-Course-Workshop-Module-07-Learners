pipeline {
    agent none

    stages {
        stage('C# build') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/core/sdk' }
            }
            environment {
                DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
            }
            steps {
                sh 'dotnet build'
            }
        }
        stage('C# test') {
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
        stage('Typescript build') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web && npm install'
                sh 'cd DotnetTemplate.Web && npm run build'
            }
        }
        stage('Typescript lint') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web && npm install'
                sh 'cd DotnetTemplate.Web && npm run build'
                sh 'cd DotnetTemplate.Web && npm run lint'
            }
        }
        stage('Typescript test') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd DotnetTemplate.Web && npm install'
                sh 'cd DotnetTemplate.Web && npm run build'
                sh 'cd DotnetTemplate.Web && npm t'
            }
        }
    }
}