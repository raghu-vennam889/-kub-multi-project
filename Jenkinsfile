pipeline {
    agent any
    stages {
        stage('Build App') {
            steps {
                sh 'echo "Building Sa-Frontend"'
                sh 'cd ${WORKSPACE}/sa-frontend && npm install && npm run build'
                sh 'echo "Building Sa-webapp"'
                sh 'cd ${WORKSPACE}/sa-webapp && mvn install'
            }
        }
        stage('Build Images') {
            steps {
                sh 'echo "Creating fronted Image"'
                sh 'cd ${WORKSPACE}/sa-frontend && docker build -t sa-frontend:"$BUILD_NUMBER" .'
                sh 'echo "Frontend Image created"'
                sh 'echo "Creating webapp Image"'
                sh 'cd ${WORKSPACE}/sa-webapp && docker build -t sa-webapp:"$BUILD_NUMBER" .'
                sh 'echo "Webapp Image Created"'
                sh 'echo "Creating sa-logic image"'
                sh 'cd ${WORKSPACE}/sa-logic && docker build -t sa-logic:"$BUILD_NUMBER" .'
                sh 'echo "sa-logic image created"'

            }
        }
        stage('push to docker'){
             steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pw', usernameVariable: 'user')]){
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" raghuram889/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker tag sa-webapp:"$BUILD_NUMBER" raghuram889/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" raghuram889/sa-logic:"$BUILD_NUMBER"'
                sh 'docker push raghuram889/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker push raghuram889/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker push raghuram889/sa-logic:"$BUILD_NUMBER"'
                }
            }
        }
     }
}
deocker
