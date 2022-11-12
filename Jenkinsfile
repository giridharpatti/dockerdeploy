pipeline {
  agent {
    label 'ubuntu'
  }
  environment{
     CODEDIR='/home/ubuntu/jenkins/workspace/nagarro_deploy/dockerdeploy'    
    }
  stages {
     stage('clone repo') {
       steps {
        sh "rm -rf *"
        sh "git clone -b develop git@github.com:giridharpatti/dockerdeploy.git"
       }
     }
    stage('Build') {
      steps {
        dir("${env.CODEDIR}") {
        echo 'Building docker image'
        sh '''
        sudo aws s3 cp docker-compose.yml s3://s3bucketasdockerimagesstorage/docker-compose.yml &&
        sudo aws lambda invoke --function-name newtargetip --invocation-type Event response.json
        '''
        }
      }
    }
  }
}
