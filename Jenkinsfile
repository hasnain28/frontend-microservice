pipeline {
  agent any
  environment {
		registryCredential = 'dockerhub'
	}
  stages {
    stage('Build') {
			steps {
				dir('frontend-node'){
					sh 'docker build -t hasnainzaib/why'
				}
			}
		}
    stage('Test') {
      steps {
			dir('frontend-node'){
				sh 'docker container run --rm -p 8098:8080 --name node -d hasnainzaib/why'
				sh 'sleep 15'
// 				sh 'curl -I http://localhost:8097'
			}
		}
	}
    stage('Publish') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						sh 'docker push hasnainzaib/why'
					}
				}
			}
		}
	}
}