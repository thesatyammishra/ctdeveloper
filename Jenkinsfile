pipeline {
	    agent any
	    tools {
	        maven 'maven'   
	        }
	    stages {
	        stage ('Git Checkout') {
	            steps {
	                git branch: 'main',
			credentialsId: '6cd486ea-6893-4acf-a418-d5dceef2be8f',
			url: 'https://github.com/thesatyammishra/ctcode.git'
	                
	                }
	            } 
		stage ('Compile') {
	            steps {
	                sh 'mvn compile'
	                }
	            }      
	        stage ('Package') {
	            steps {
	                sh 'mvn package'
	                }
	            }
	        stage ('Install') {
	            steps {
	                sh 'mvn install'
	                }
	            }
		 stage ('Test') {
	            steps {
			sh 'cd /root/.jenkins/workspace/new1/ && touch test-results-unit.xml'    
	                sh 'mvn test'
	                }
			 post {
			 always {
				   junit '**/test-results-unit.xml'	
			 }
	            }   
		 }
		    
		 stage ('Create war file') {
	            steps {
	                sh 'jar -cf target/dependency/webapp-runner.jar target/*.war'
	                }
	            }
		    
                stage ('Deploy War File') {
                        steps {
                                sh "cp target/*.war /home/ec2-user/apache-tomcat-8.5.61/webapps/"
                        }
                }
	}
}
