pipeline {
    agent any
     environment {
		dockerhub=credentials('dockerhub')
	}   
    stages{
        stage('Build Maven'){
            steps{
                //checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sankardevvinu/devops-automation.git']]])
                git branch: 'main', url: 'https://github.com/sankardevvinu/projectsupport.git'
                
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t java/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   //withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   //sh 'docker login -u javatechie -p ${dockerhubpwd}'
                   sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin docker.io'
}
                   sh 'docker push java/devops-integration'
                }
            }
        }
    }

