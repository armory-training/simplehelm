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
           source bin/env
           . /mnt/secrets/bintray/bintray
           ./bin/push
           ''' 
         archiveArtifacts artifacts: 'build.properties'
        }
      }
    }
}
