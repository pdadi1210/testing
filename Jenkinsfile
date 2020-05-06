pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'building docker image'
                sh '''
                    pip install -r requirements.txt -t .
					python -m unittest test
					aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 500210368645.dkr.ecr.us-east-1.amazonaws.com/helloworldrepo
					docker build -t helloworldrepo .
					docker tag helloworldrepo:latest 868551682415.dkr.ecr.us-east-2.amazonaws.com/python-helloworld
					docker push 868551682415.dkr.ecr.us-east-2.amazonaws.com/python-helloworld
					kubectl apply -f kubernetes.yaml
                '''
            }
        }
    }
}