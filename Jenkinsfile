pipeline {
    agent {
        docker {
            label 'docker-agent'
            image 'registry02.homelab.internal:8443/jenkins/jenkins-agent:jdk21-patched'
            registryUrl 'https://registry.midominio.com'
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