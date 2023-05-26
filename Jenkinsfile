pipeline {
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Priya222-sudo/jenkins-mvn-docker.git']]])
                sh 'mvn clean install'
            }
        }
    
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t priyankasonone7410/devops-integration1 .'
                }
            }
        }
         stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u priyankasonone7410 -p ${dockerhubpwd}'

                      }
                   sh 'docker push priyankasonone7410/devops-integration1'
                }
            }
        }
    }
}
