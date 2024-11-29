pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('docker credentials') // Your Docker Hub credentials
        AWS_REGION = 'us-east-1'  // Set the region
        CLUSTER_NAME = 'my-eks-cluster'  // Set your EKS cluster
    }

    stages {
        stage('Configure Kubeconfig') {
            steps {
                script {
                    // Make sure AWS CLI is installed and AWS credentials are configured
                    sh "aws eks --region ${AWS_REGION} update-kubeconfig --name ${CLUSTER_NAME}"
                }
            }
        }  // Close the 'Configure Kubeconfig' stage

        stage('DockerHub Login') {
            steps {
                script {
                    sh '''
                        echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin
                    '''
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                sh '''
                    echo "Building Docker images..."
                    docker build -t ahmed862/frontend frontend/.
                    docker build -t ahmed862/backend backend/.
                '''
            }
        }

        stage('Push Docker Images') {
            steps {
                sh '''
                    echo "Pushing Docker images..."
                    docker push ahmed862/frontend
                    docker push ahmed862/backend
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying to eks cluster..."
                // Use the kubeconfig stored as a Jenkins credential
                withCredentials([file(credentialsId: 'eks', variable: 'KUBECONFIG')]) {
                    sh '''
                        kubectl apply -f k8s/front.yaml
                        kubectl apply -f k8s/backend.yaml
                        kubectl apply -f k8s/mongodebloyment.yaml
                        kubectl apply -f k8s/pv.pvc.yaml
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Deployment was successful!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}
