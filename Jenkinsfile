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
docker build -t beripavankumar214/flask-app:latest -f docker/Dockerfile .
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

```
    withCredentials([
        usernamePassword(
            credentialsId: 'dockerhub',
            usernameVariable: 'USER',
            passwordVariable: 'PASS'
        )
    ]) {

        sh '''
        echo "$PASS" | docker login \
        -u "$USER" \
        --password-stdin

        docker push $DOCKER_IMAGE
        '''
    }
}
```

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