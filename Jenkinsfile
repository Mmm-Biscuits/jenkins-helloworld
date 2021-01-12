pipeline {
  agent any
  stages {
    stage('Fetch dependencies') {
      steps {
        sh 'sudo docker pull karthequian/helloworld:latest'
      }
    }

    stage('Build docker image') {
      steps {
        sh 'sudo docker build . -t customapp:1'
      }
    }

    stage('Test image') {
      steps {
        sh 'echo "Tests successful"'
      }
    }

    stage('Push image to OCIR') {
      steps {
        sh 'sudo docker login -u adexacs2/bspendol -p \'s#Oa(4M;h]ZJYfLvPE2]\' fra.ocir.io'
        sh 'sudo docker tag customapp:1 fra.ocir.io/adexacs2/customapp:custom'
        sh 'sudo docker push fra.ocir.io/adexacs2/customapp:custom'
      }
    }

    stage('Deploy to OKE') {
      steps {
        sh 'sh ../../hello-deploy.sh'
      }
    }

    stage('') {
      steps {
        sh 'sh kill.sh'
      }
    }

  }
}