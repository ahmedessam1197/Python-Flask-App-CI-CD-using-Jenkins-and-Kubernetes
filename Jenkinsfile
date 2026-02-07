pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ahmed277/pro-app"
        DOCKER_CREDENTIALS = "dockerhub-creds"
    }

    stages {

        stage("Build Docker Image") {
            steps {
                sh "docker build -t $DOCKER_IMAGE:${BUILD_NUMBER} ."
            }
        }

        stage("DockerHub Login") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: DOCKER_CREDENTIALS,
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo "Logging in user: $DOCKER_USER"
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage("Push Image") {
            steps {
                sh "docker push $DOCKER_IMAGE:${BUILD_NUMBER}"
            }
        }

        stage("Deploy to Kubernetes") {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-creds', variable: 'KUBECONFIG')]) {
                    sh "kubectl apply -f k8s/deployment.yaml"
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline Deployed successfully"
        }
        failure {
            echo "Pipeline Deployed failed"
        }
    }
}
