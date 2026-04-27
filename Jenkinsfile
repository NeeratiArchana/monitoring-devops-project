pipeline {
    agent any

    environment{
        DOCKER_USER = "neeratiarchana"
	IMAGE_NAME = "monitoring-app"
    }
    stages{
	stage('Clone code'){
	    steps {
		git branch: 'main', url: 'https://github.com/NeeratiArchana/monitoring-devops-project.git'
	    }
	}
	stage('build Docker Image'){
	    steps{
		sh 'docker build -t $DOCKER_USER/$IMAGE_NAME:latest .'
	    }
	}
	stage('Push to DockerHub'){
	    steps{
		withCredentials([usernamePassword(credentialsId: 'docker-pass', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
		    sh '''
		    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin 
		    docker push $DOCKER_USER/$IMAGE_NAME:latest
		    '''
		}
	    }
	}
	stage('Deploy to kubernetes'){
	    steps{
		sh '''
		kubectl apply -f deployment.yaml
		kubectl apply -f service.yaml
		'''
 	    }
        }
    }
}
