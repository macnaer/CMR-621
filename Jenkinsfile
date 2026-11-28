pipeline {
    agent any

    environment {
        IMAGE_NAME = "demo_ci_site"
    }

    stages {
        stage("Build Docker Image") {
            steps {
                sh "docker build --no-cache -t ${IMAGE_NAME}:${env.BUILD_NUMBER} ."
            }
        }

        stage("Deploy Website") {
            steps {
                sh """
                    docker stop demo_ci_container || true
                    docker rm demo_ci_container || true
                    docker run -d --name demo_ci_container --restart=always -p 8088:80 ${IMAGE_NAME}:${env.BUILD_NUMBER}
                """
            }
        }
    }
}
