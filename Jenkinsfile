pipeline{
    agent{
        label "jenkins-agent1"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
    }
    environment{
        APP_NAME = "dmistry-complete-jenkins-prod-e2e-pipeline"
        RELEASE = "1.0.0"
        DOCKER_USER="sampathdockerid"
        DOCKER_PASSWORD="dockerhub-secret"
        IMAGE_NAME="${DOCKER_USER}" + "/" + "{$APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }
    stages{
        stage("cleanup workspace"){   
            steps{
                cleanWs()
            }
        }
        stage("Checkout from SCM"){   
            steps{
                git branch: 'main', url: 'https://github.com/samjax/dmistry-complete-jenkins-prod-e2e-pipeline.git'
            }
        }
        stage("Build application"){   
            steps{
                sh 'mvn clean package'
            }
        }
        stage("Test application"){   
            steps{
                sh 'mvn test'
            }
        }
        stage("Build and push Docker image"){
            steps{
                script{
                    docker.withRegistry('',DOCKER_PASSWORD){
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('', DOCKER_PASSWORD){
                        docker_image.push("${IMAGE_TAG}")
                    }
                }

            }
        }
    }
}