pipeline {
    agent any

    environment{
        DOCKER_USER = "your-docker-username"
	IMAGE_NAME = "monitoring-app"
    }
    stages{
	stage('Clone code'){
	    steps {
		git 'https://github.com/NeeratiArchana/monitoring-devops-project.git'
	    }
	}
	stage('build Docker Image'){
	    steps{
		sh 'docker buils -t $DOCKER_USER/4IMAGE_NAME:latest .'
	    }
	}
	stage('Push to DockerHub'){
	    steps{
		withCredentials([string(credentialsId: 'docker-pass', variable: 'DOCKER_PASS')]){
		    sh '''
		    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin 
		    docker push $DOCKER_USER/$IMAGE_NAME:latest
		    '''
		}
	    }
	}
    }
}
