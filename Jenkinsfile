pipeline {
    agent any
     environment {
		dockerhub=credentials('docker')
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
                    sh "docker build -t sankardev/task:version2 ."
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   //withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker tag sankardev/task:version2 vinuinstinct123/sankardev:version2'
                   sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin docker.io'
}
                   sh 'docker push vinuinstinct123/sankardev:version2'
                }
            }
        }
    }

