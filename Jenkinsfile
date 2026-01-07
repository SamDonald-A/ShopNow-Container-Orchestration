pipeline {
    agent any

    environment {
        DOCKERHUB_REPO = "samdonalda"
        FRONTEND_IMAGE = "shopnow-frontend"
        BACKEND_IMAGE  = "shopnow-backend"
        HELM_RELEASE   = "shopnow"
        NAMESPACE      = "shopnow-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Images') {
            steps {
                script {
                    echo "Building Docker images..."
                    docker.build("${DOCKERHUB_REPO}/${FRONTEND_IMAGE}:latest", "frontend")
                    docker.build("${DOCKERHUB_REPO}/${BACKEND_IMAGE}:latest", "backend")
                    echo "Docker images built successfully!"
                }
            }
        }

        stage('Push Images') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'docker-hub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                      echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                      docker push ${DOCKERHUB_REPO}/${FRONTEND_IMAGE}:latest
                      docker push ${DOCKERHUB_REPO}/${BACKEND_IMAGE}:latest
                    '''
                    echo "Docker images pushed successfully!"
                }
            }
        }

        stage('Deploy to EKS using Helm') {
            steps {
                sh '''
                  echo "Deploying Helm chart..."
                  helm upgrade --install ${HELM_RELEASE} ./shopnow-helm \
                    --namespace ${NAMESPACE} \
                    --create-namespace
                  echo "Helm chart deployed successfully!"
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                  echo "Listing all pods in namespace ${NAMESPACE}..."
                  kubectl get pods -n ${NAMESPACE} -o wide
                  
                  echo "Listing all services..."
                  kubectl get svc -n ${NAMESPACE}
                  
                  echo "Listing ingress / load balancer..."
                  kubectl get ingress -n ${NAMESPACE}
                '''
            }
        }

        stage('Show Pod Logs (Optional)') {
            steps {
                sh '''
                  echo "Showing last 50 lines of logs for backend pod..."
                  BACKEND_POD=$(kubectl get pods -n ${NAMESPACE} -l app=backend -o jsonpath="{.items[0].metadata.name}")
                  kubectl logs $BACKEND_POD -n ${NAMESPACE} --tail=50
                  
                  echo "Showing last 50 lines of logs for frontend pod..."
                  FRONTEND_POD=$(kubectl get pods -n ${NAMESPACE} -l app=frontend -o jsonpath="{.items[0].metadata.name}")
                  kubectl logs $FRONTEND_POD -n ${NAMESPACE} --tail=50
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully! All services are running."
        }
        failure {
            echo "Deployment failed. Check Jenkins logs for details."
        }
    }
}
