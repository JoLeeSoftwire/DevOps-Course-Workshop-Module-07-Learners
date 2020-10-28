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
    post {
        success {
            slackSend channel: '#jos-test-website',
            color: 'good',
            message: "the site built happily on ${currentBuild.fullDisplayName}"

        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            slackSend channel: '#jos-test-website',
            color: 'danger',
            message: "the site did not build, sadface :( on ${currentBuild.fullDisplayName}"
        }
        changed {
            slackSend channel: '#jos-test-website',
            color: 'warning',
            message: "this was a change, maybe party, maybe not on ${currentBuild.fullDisplayName}"
        }
    }
}