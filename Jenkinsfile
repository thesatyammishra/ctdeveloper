pipeline {
	    agent any
	    tools {
	        maven 'maven'
		ant 'ant'   
	        }
	    stages {
	        stage ('Git Checkout') {
	            steps {
	                git branch: 'main',
			credentialsId: '26d7f9d5-5345-44c9-aa0d-8bc3fbb0aff7',
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
		    
		 stage ('Create war file') {
	            steps {
	                sh 'jar -cf target/dependency/webapp-runner.jar target/*.war'
	                }
	            }
		    
                stage ('Deploy War File') {
                        steps {
                                sh "cp target/*.war /root/apache-tomcat-9.0.41/webapps/"
                        }
                }
	}
}
