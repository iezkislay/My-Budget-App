pipeline {
    agent any

    stages {
        stage('Repo Clone') {
            steps {
                script {
                    // Define the repository URL
                    def repoUrl = 'https://github.com/iezkislay/My-Budget-App.git'

                    // Checkout the repository to a specific directory
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: repoUrl]]])
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                // Run the Docker build command
                sh 'docker build -t budget-app /var/lib/jenkins/workspace/${JOB_NAME}/My-Budget-App'
            }
        }
        stage('Run Docker Container') {
            steps {
                // Run the Docker build command
                sh 'docker stop budget || true'
                sh 'docker rm budget || true'
                sh 'docker run -dt --name budget -p 3000:3000 -e DATABASE_URL=postgres://budgy:yourpassword@localhost:5432/Budgy_development budget-app'
            }
        }
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
    }
}
