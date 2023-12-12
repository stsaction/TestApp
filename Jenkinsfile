pipeline {
    agent none
    
    parameters {
        choice(name: 'AGENT', choices: ['Test', 'Test2'], description: 'choose the node agent')
        string(name: 'Trigger_Repo', description: 'Enter the Git URL')
    }
    
    stages {
        stage('Preparation') {
            agent any
            steps {
                cleanWs() // Clean up the workspace before starting the pipeline
            }
        }

        stage('Checkout') {
            agent { label "${params.AGENT}" }
            steps {
                //script {
                    // Ensure the 'git' tool is configured
                    //def scmVars = checkout scm
                }
            }
        }

        stage('Docker Compose Down') {
            agent any
            steps {
                script {
                    // Stop and remove Docker containers
                    sh 'docker-compose down'
                }
            }
        }

        stage('Docker Compose Up') {
            agent any
            steps {
                script {
                    // Start Docker containers
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Restart Nginx') {
            agent any
            steps {
                script {
                    // Restart Nginx (assuming it is one of the services defined in your docker-compose.yml)
                    sh 'sudo systemctl restart nginx'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
