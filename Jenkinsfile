pipeline {

agent any

environment {
DOCKER_IMAGE='beripavankumar214/flask-app'
}

stages {

stage('Checkout') {

steps {
git branch: 'main',
url: 'https://github.com/pavaniam214/jenkins-cicd-project.git'
}

}

stage('Build') {
steps {
sh '''
docker build 
-t dockerhub-user/flask-app 
-f docker/Dockerfile .
'''
}
}


stage('Test') {

steps {

sh '''
echo Testing Complete
'''

}

}

stage('Push Image') {

steps {

withCredentials([
usernamePassword(
credentialsId:'dockerhub',
usernameVariable:'beripavankumar214',
passwordVariable:'Pavaniam214@'
)

]) {

sh '''
docker login -u $beripavankumar214 -p $Pavaniam214@

docker push $DOCKER_IMAGE
'''

}

}

}

stage('Deploy') {

steps {

sh '''
kubectl apply -f k8s/
'''
}

}

}

}