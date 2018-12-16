pipeline {
  agent any
    stages {
      stage("Build Image") {
        steps {
          sh '''
            source bin/env
            ./bin/build
            '''
        }
      }

      stage("Push Image") {
        when { branch 'master' }
        steps {
         sh '''#!/bin/bash +x
           . /mnt/secrets/bintray/bintray
           AWS_ACCESS_KEY=$(aws --profile armory-ps-prod configure get aws_access_key_id) \
           AWS_SECRET_KEY=$(aws --profile armory-ps-prod configure get aws_secret_access_key) \
           ./bin/push
           ''' 
         archiveArtifacts artifacts: 'build.properties'
        }
      }
    }
}
