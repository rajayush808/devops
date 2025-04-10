pipeline {
    agent any  // Use any available agent
    
    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }   // this has to be added only if you get an error saying UTF required is 8 but showing in ISO00009

    tools {
        maven 'Maven'  // Ensure this matches the name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rajayush808/devops.git'
            }
        }

        stage('Build') {
        	 steps {
                	sh 'mvn clean package'  // Run Maven build
            }
        }

     	stage('Archive') {
            	steps {
                	archiveArtifacts artifacts: 'target/*.war', fingerprint:true
            }	
        }
        stage('Deploy') {
            steps {
               sh 'mvn clean package'  
               sh 'ansible-playbook playbook.yml -i hosts.ini'
            }
        }
     }
 }
      


