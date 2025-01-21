pipeline {
    agent {
        label "docker-node" // Ensures the pipeline runs on a node labeled "docker-node"
    }

    stages {
        stage("Checkout") {
            steps { 
                echo "Checking out the code"
                checkout scm // Checks out the code from the repository configured in Jenkins
            }
        }

        stage("Building") {
            steps { 
                echo "Building Docker images"
                sh "docker-compose build" // Builds the Docker images defined in docker-compose.yaml
            }
        }

        stage("Testing") {
            steps {
                echo "Testing the application"
                sh "flask --version && pip install -r requirements.txt" // Corrected testing command and installation of dependencies
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the application"
                sh "docker-compose down" // Stops and removes running containers
                sh "docker-compose up --build -d" // Rebuilds and runs containers in detached mode
            }
        }
    }

    post {
        always {
            echo "This will always run, regardless of success or failure"
        }
        success {
            echo "CI/CD pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check the logs for details."
        }
    }
}
