pipeline {
	agent any
	    stages {
	        stage('Build test') {
	            steps {
                	script {
                  		test = docker.build("tg5688/multicontainer-test", "-f client/Dockerfile.dev .")
                  		test.inside{
                    			sh 'npm run test'
                  		}
                	}
	            }
	        }
	    }
	}
