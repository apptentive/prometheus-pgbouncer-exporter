#!/groovy
// apptentive.*() functions tracked in github and imported as 'immutable-shared'
//   https://github.com/apptentive/jenkins-shared-libs/tree/master/vars
@Library('immutable-shared') _


pipeline {
  agent {
    kubernetes {
      yamlFile './_cri/KubernetesBuildPod.yaml'
    }
  }  

  options {
    timeout(time: 10, unit: 'MINUTES')
  }

  stages {
    stage('Dev') {
      when {
        expression { env.ENVIRONMENT == 'dev' }
      }

      stages {
        stage('build'){
          steps {
            script {
              gitCommit = apptentiveGetReleaseCommit()
              imageName = apptentiveDockerBuild('build', "latest")
            }
          }
        }
      }
    }
  }
}
