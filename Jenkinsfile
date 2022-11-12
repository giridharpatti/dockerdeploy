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
        sudo sed -i 's/imageversion/$version/g' docker-compose.yml &&
        sudo aws s3 cp docker-compose.yml s3://s3bucketasdockerimagesstorage/docker-compose.yml &&
        sudo aws lambda invoke --function-name newtargetip --invocation-type Event --region ap-south-1 response.json
        '''
        }
      }
    }
  }
}
