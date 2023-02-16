pipeline {
	agent any
	stages {
	    stage ('clean up') {
	        steps {
	            cleanWs()
	        }
	    }
	    
	    stage ('clone') {
			steps {
				sh 'git clone https://github.com/sunilnl18/java-maven-app.git'
			}
	    }
		stage ('build') {
			steps {
			    dir ('java-maven-app'){
				    sh 'mvn clean install -DskipTests'
			    }
			}
		
		}
		stage ('test') {
			steps {
			    dir ('java-maven-app') {
				    sh 'mvn test'
			    }
			}
			post {
				always {
				    dir ('java-maven-app') {
					    junit 'target/surefire-reports/*.*xml'
				    }
				}
			}
		}
		stage ('run') {
			steps {
			    dir ('java-maven-app') {
			    	sh './scripts/deliver.sh'
			    }
			}
		
		}
	}
}
