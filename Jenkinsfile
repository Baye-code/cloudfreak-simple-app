pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JAVA8'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                    sh 'pwd'
		                sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('acrimghub/petclinic', "./docker")
                 docker.withRegistry('https://acrimghub.azurecr.io', 'acrimghub-creds') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
