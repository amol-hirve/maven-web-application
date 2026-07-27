pipeline
{
    agent any

    tools
    {
        maven 'Maven_3.9.15'
    }

    environment
    {
        buildNumber = "${BUILD_NUMBER}"
    }

    stages
    {
        stage('Git Checkout')
        {
            steps()
            {
                git branch: DevOpsApril2026, url: 'https://github.com/MithunTechnologiesDevOps/Maven-Web-Application.git'
            }
        }

        stage('Build Artifact')
        {
            steps()
            {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image')
        {
            steps()
            {
                sh 'docker build -t mithuntechnologies/login-service:${buildNumber} .'
            }
        }

        stage('Push Docker Image to DockerHub')
        {
            steps()
            {
                withCredentials([string(credentialsId: 'Docker_Hub_Secret', variable: 'Docker_Hub_Secret')])
                {
                    sh 'docker push mithuntechnologies/login-service:${buildNumber}'
                }
            }
        }

        stage('Remove Docker Image from Jenkins Local')
        {
            steps()
            {
                sh 'docker rmi -f mithuntechnologies/login-service:${buildNumber}'
            }
        }
    }
}