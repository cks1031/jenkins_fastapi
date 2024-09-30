pipeline {
    agent any

    environment {
		DOCKERHUB_SECRETS=credentials('dockerhub')
        IMAGE_NAME = 'nanakia1031/jenkins_nodejs3'
        IMAGE_TAG = 'latest'
    }
    
    stages {
        stage('clone from SCM'){
			steps{
				git url: 'https://github.com/cks1031/jenkins_fastapi.git', branch: 'main'
			  }
		  }
        stage('Build Docker Image') {
            steps {
                sh '''
				docker compose build
				'''                
            }
        }

        stage('Loggin into Docker Hub') {
            steps {                             
				sh '''
				echo ${DOCKERHUB_SECRETS_PSW} | docker login -u ${DOCKERHUB_SECRETS_USR} --password-stdin
				'''
            }
        }

        stage('Pushing Docker Image to Docker Hub') {
            steps {
                sh '''
				docker tag cks1031/nodejs-app ${IMAGE_NAME}:${IMAGE_TAG}
                docker push ${IMAGE_NAME}:${IMAGE_TAG}
				'''
            }
        }

        stage('Docker Hub logout') {
            steps {
                sh '''
				docker logout
				'''
            }
        }
    }
}
