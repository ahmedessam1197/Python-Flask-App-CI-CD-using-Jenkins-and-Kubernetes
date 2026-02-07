pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ahmed277/pro-app"
        DOCKER_CREDENTIALS = "pro-app"
        KUBE_CONFIG = "/home/jenkins/.kube/config"
    }

    stages {

        stage("Build Docker Image") {
            steps {
                script {
                    sh """
                    docker build -t $DOCKER_IMAGE:${BUILD_NUMBER} .
                    """
                }
            }
        }

        stage("DockerHub Login") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: DOCKER_CREDENTIALS,
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                }
            }
        }

        stage("Push Image") {
            steps {
                sh """
                docker push $DOCKER_IMAGE:${BUILD_NUMBER}
                """
            }
        }

        stage("Deploy to Kubernetes") {
            steps {
                sh """
                export KUBECONFIG=$KUBE_CONFIG
                envsubst < k8s/deployment.yaml | kubectl apply -f -
                """
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
