pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/lotfy74/devops-automation.git']]])                
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t amr8/devops-automation:1.0 .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                   sh 'docker login -u ${USER} -p ${PASS}'

}
                   sh 'docker push amr8/devops-automation:1.0 '
               }
           } 
        } 
    }
}
