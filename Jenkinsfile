pipeline {
    agent any
    
     environment {
		dockerhub=credentials('docker')
	}   
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sankardevvinu/devops-automation.git']]])
                //git branch: 'main', url: 'https://github.com/sankardevvinu/devops-automation.git'
		
                sh 'mvn package'
            
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
                   sh 'docker tag sankardev/task:version2 vinuinstinct123/sankardev:version2'
                   sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin docker.io'
                   sh 'docker push vinuinstinct123/sankardev:version2'
                }
            }
        }
	stage('Deploy to cluster') {
          steps {
             script { 
	       kubernetesDeploy(configs:"deploymentservice.yaml",kubeconfigId:"kubernetes")
        }
      }
    }		 
}
}
