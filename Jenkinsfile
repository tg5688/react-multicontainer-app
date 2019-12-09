pipeline {
	    agent any
	    stages {
	        stage('Build test') {
	            steps {
                script {
                  test = docker.build("tg5688/multicontainer-test", "-f Dockerfile.dev ./client")
                  test.inside{
                    sh 'npm run test'
                  }
                }
	            }
	        }
	        stage('Build Docker Images) {
	            steps {
                client = docker.build("tg5688/multicontainer-client", "./client")
                nginx = docker.build("tg5688/multicontainer-nginx", "./nginx")
                server = docker.build("tg5688/multicontainer-server", "./server")
                worker = docker.build("tg5688/multicontainer-worker", "./worker")
	            }
	        }
	        stage('Push Docker Image') {
	            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login') {
                        client.push("${env.BUILD_NUMBER}")
                        client.push("latest")
                        nginx.push("${env.BUILD_NUMBER}")
                        nginx.push("latest")
                        server.push("${env.BUILD_NUMBER}")
                        server.push("latest")
                        worker.push("${env.BUILD_NUMBER}")
                        worker.push("latest")
                    }
                }
	            }
	        }
	    }
	}
