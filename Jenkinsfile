pipeline {

agent any

environment {
DOCKER_IMAGE='dockerhub-user/flask-app'
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
docker build -t $DOCKER_IMAGE .
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
usernameVariable:'USER',
passwordVariable:'PASS'
)

]) {

sh '''
docker login -u $USER -p $PASS

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