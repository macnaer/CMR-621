#!groovy

pipeline {
    agent any

    environment {
        IMAGE_NAME = "macnaer/website"
    }

    stages {

        stage("Build website image") {
            steps {
                echo 'Building Demosite image ...'
                sh """
                    docker build --no-cache -t ${IMAGE_NAME}:${env.BUILD_NUMBER} .
                """
            }
        }


        stage("Deploy Demo site") {
            steps {
                echo "Deploying Demo site ..."  
                sh """
                    docker stop website || true
                    docker rm website || true
                    docker run -d --name website --restart=always -p 80:80 macnaer/website:${env.BUILD_NUMBER}
                    docker image prune -f
                """
            }
        }

    }
}
