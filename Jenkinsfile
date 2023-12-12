pipeline {
    agent none
    
    parameters {
        choice(name: 'AGENT', choices: ['Test', 'Test2'], description: 'choose the node agent')
        string(name: 'Trigger_Repo', description: 'Enter the Git URL')
    }
    
    stages {
        stage('Checkout') {
            agent { label "${params.AGENT}" }
            steps {
                git url: "${params.Trigger_Repo}" // Corrected parameter name
                
            }  
        }

        stage('Docker Compose Down') {
            steps {
                script {
                    // Stop and remove Docker containers
                    sh 'docker-compose down'
                }
            }
        }

        stage('Docker Compose Up') {
            steps {
                script {
                    // Start Docker containers
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Restart Nginx') {
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
