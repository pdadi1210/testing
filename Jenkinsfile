pipeline{
  agent any
  stages{
      stage('testing'){
          steps{
              git branch: 'master', credentialsId: 'pdadi1210', url: 'https://github.com/pdadi1210/testing.git'
              sh 'pip3 install -r requirements.txt -t .'
              sh 'python3 -m unittest test'
          }
      }
stage('SSH transfer') {
steps{
 sh "zip -r sample.zip *"
 git branch: 'master', credentialsId: 'pdadi1210', url: 'https://github.com/pdadi1210/testing.git'
 script {
  sshPublisher(
   continueOnError: false, failOnError: true,
   publishers: [
    sshPublisherDesc(
     configName: "eks-cluster-integration",
     verbose: true,
     transfers: [
      sshTransfer(
       sourceFiles: "sample.zip",
       removePrefix: "",
       remoteDirectory: "",
       execCommand: "mkdir -p sample && rm -rf sample/* && unzip sample.zip -d sample && cd sample && docker build -t helloworldrepo . && docker tag helloworldrepo:latest 868551682415.dkr.ecr.us-east-2.amazonaws.com/python-helloworld && docker push 868551682415.dkr.ecr.us-east-2.amazonaws.com/python-helloworld && kubectl apply -f deployment.yaml "
      )
     ])
   ])}
 }
}
}}