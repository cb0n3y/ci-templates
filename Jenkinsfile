pipeline {
    agent {
        docker {
            label 'docker-agent'
            image 'registry02.homelab.internal/jenkins/jenkins-agent:latest'
            registryUrl 'https://registry02.homelab.internal'
            registryCredentialsId 'harbor-credentials'
            alwaysPull true
        }
    }

    stages {
        stage('Checkout') {
            steps {
                cleanWs()
                echo "Fetching repository..."
                checkout scm
                sh 'mkdir -p build'
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    echo "Repository successfully cloned."
                    pwd
                    ls -lh
                '''
            }
        }
    }

    post {
        success {
            cleanWs()
        }
    }
}