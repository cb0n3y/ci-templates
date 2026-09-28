pipeline {
    agent {
        docker {
            label 'docker-agent'
            image 'registry02.homelab.internal/jenkins/jenkins-agent:latest'
            registryUrl 'https://registry02.homelab.internal'
            registryCredentialsId 'jx-laptop'
            alwaysPull true
        }
    }

    options {
        timeout(time: 15, unit: 'MINUTES')
        buildDiscarder(logRotator(numToKeepStr: '20'))
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

        stage('Lint') {
            parallel {
                stage('YAML')    { steps { sh 'scripts/lint-yaml.sh' } }
                stage('Bash')    { steps { sh 'scripts/lint-bash.sh' } }
                stage('Python')  { steps { sh 'scripts/lint-python.sh' } }
                stage('Actions') { steps { sh 'actionlint' } }
            }
        }
    }

    post {
        success {
            cleanWs()
        }
    }
}