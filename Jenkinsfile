pipeline {
    agent any
    stages {

        stage('Clone Repo') {
          steps {
            sh 'rm -rf dockertest1'
            sh 'git clone https://github.com/nareshmanojari1/dockertest1.git'
            }
        }

        stage('Build Docker Image') {
          steps {
            sh 'cd /var/lib/jenkins/workspace/pipeline2/dockertest1'
            sh 'cp  /var/lib/jenkins/workspace/pipeline2/dockertest1/* /var/lib/jenkins/workspace/pipeline2'
            sh 'docker build -t sreeharshav/pipelinetest:v1 .'
            }
        }

        stage('Push Image to Docker Hub') {
          steps {
           sh    'docker push nareshmanojari1/pipelinetest:v1'
           }
        }

        stage('Deploy to Docker Host') {
          steps {
            sh    'docker -H tcp://10.1.1.200:2375 stop webapp1'
            sh    'docker -H tcp://10.1.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 sreeharshav/pipelinetest:v1'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh 'sleep 10s'
          sh 'curl ec2-18-213-116-200.compute-1.amazonaws.com:9000'
          }
        }

    }
}
