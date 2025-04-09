pipeline{
    agent{
        label "jenkins-agent1"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
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
    }
}