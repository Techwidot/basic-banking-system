pipeline {
    agent any
    
    stage('Checkout Git Repo') {
            steps {
                script {
                    // Define the Git URL (HTTP/HTTPS)
                    def gitURL = 'https://github.com/Techwidot/basic-banking-system.git'

                    // Checkout the Git repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: gitURL]]])
                }
            }
        }
        
        stage('Build and Test') {
            steps {
                // Install Node.js and npm (if not already done)
                // Use Maven to build and test the Node.js application
                sh 'mvn clean install'
            }
        }

        stage('Static Code Analysis') {
            steps {
                // Run SonarQube analysis
                // Assumes SonarQube is configured in Jenkins
                withSonarQubeEnv('Your_SonarQube_Server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Containerize (Docker)') {
            steps {
                // Build a Docker image for the Node.js app
                sh 'docker build -t your-docker-image-name .'
                // Push the Docker image to a registry (if needed)
                // sh 'docker push your-docker-image-name'
            }
        }

        stage('Deploy (Kubernetes)') {
            steps {
                // Deploy the Docker container to Kubernetes
                sh 'kubectl apply -f kubernetes-deployment.yaml'
            }
        }

        stage('Finalize') {
            steps {
                // Additional steps like notifications or cleanup
            }
        }
    }
    
    post {
        success {
            // Perform actions on successful deployment
        }
        failure {
            // Perform actions on pipeline failure
        }
    }
}
