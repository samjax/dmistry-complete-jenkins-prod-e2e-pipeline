pipeline{
    agent{
        label "jenkins-agent1"
    }
    tools{
        jdk 'Java17'
        maven 'maven3'
    }
    stages{
        stage("cleanup workspace"){   
            steps{
                cleanWs()
            }
        }
    }
    stages{
        stage("Checkout from SCM"){   
            steps{
                git branch: 'main', url: 'https://github.com/samjax/dmistry-complete-jenkins-prod-e2e-pipeline.git'
            }
        }
    }
}