pipeline {
    agent any

    stages {
        stage('Build Sa-Frontend') {
            steps {
                sh 'cd sa-frontend && npm install && npm run build'
            }
        }
        stage('Build Sa-Webapp') {
            steps {
                sh 'cd sa-webapp && mvn install'
            }
        }
        stage('Docker image') {
            steps {
                sh 'cd sa-frontend && docker build -t sa-frontend:1.0.0 .'
            }
        }
        stage('Email Notification') {
	    steps {
		emailext body: 'Build Failed. Please check the Dashboard of Jenkins', subject: 'Build Failed. Please check the Dashboard of Jenkins', to: 'raghu.vennam889@gmail.com' '12r91a0291@gmail.com'
            }
	}
    }
}
