pipeline {
    agent any

    environment {
        DOCKERHUB_REPO = "samdonalda"
        FRONTEND_IMAGE = "shopnow-frontend"
        BACKEND_IMAGE  = "shopnow-backend"

        HELM_RELEASE   = "shopnow"
        NAMESPACE      = "shopnow-app"

        AWS_REGION     = "eu-west-2"
        EKS_CLUSTER    = "sam-project-cluster"
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
                }
            }
        }

        stage('Configure Kubeconfig (EKS)') {
            steps {
                sh '''
                  echo "Configuring kubeconfig for EKS..."
                  aws eks update-kubeconfig \
                    --region ${AWS_REGION} \
                    --name ${EKS_CLUSTER}

                  echo "Verifying cluster access..."
                  kubectl get nodes
                '''
            }
        }

        stage('Deploy to EKS using Helm') {
            steps {
                sh '''
                  echo "Deploying Helm chart..."
                  helm upgrade --install ${HELM_RELEASE} ./shopnow-helm \
                    --namespace ${NAMESPACE} \
                    --create-namespace
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                  echo "Pods:"
                  kubectl get pods -n ${NAMESPACE} -o wide

                  echo "Services:"
                  kubectl get svc -n ${NAMESPACE}

                  echo "Ingress / LoadBalancer:"
                  kubectl get ingress -n ${NAMESPACE}
                '''
            }
        }

        stage('Show Pod Logs (Optional)') {
            steps {
                sh '''
                  echo "Backend logs:"
                  BACKEND_POD=$(kubectl get pods -n ${NAMESPACE} -l app=backend -o jsonpath="{.items[0].metadata.name}")
                  kubectl logs $BACKEND_POD -n ${NAMESPACE} --tail=50 || true

                  echo "Frontend logs:"
                  FRONTEND_POD=$(kubectl get pods -n ${NAMESPACE} -l app=frontend -o jsonpath="{.items[0].metadata.name}")
                  kubectl logs $FRONTEND_POD -n ${NAMESPACE} --tail=50 || true
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment completed successfully!"
        }
        failure {
            echo "❌ Deployment failed. Check logs above."
        }
    }
}
