pipeline {
    agent {
        docker {
            label 'docker-agent'
            image 'registry02.homelab.internal:8443/jenkins/jenkins-agent:latest'
            registryUrl 'https://registry02.homelab.internal'
            registryCredentialsId '1f2e9fe2-d898-49b1-a588-2b6ca0a9d30f'
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