pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/aatrika345/gitrepo2', branch: 'main', credentialsId: '03b013ca-e9a7-4fe2-a3c1-8e6f7f5af732')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t aatrika345/srepo1:latest .
sudo docker push aatrika345/srepo1:latest '''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 aatrika345/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 aatrika345/srepo1:latest'''
          }
        }

      }
    }

  }
}