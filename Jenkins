pipeline {
    agent any
    
    //stages {
        //stage('Checkout') {
          //  #steps {
             //   checkout scm
          //  }
     //   }

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
                    sh 'docker-compose restart nginx'
                }
            }
        }
    }

    post {
        always {
            // Clean up: Stop and remove Docker containers after the pipeline
            script {
                sh 'docker-compose down'
            }
        }

        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
