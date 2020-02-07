pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        sh "mkdir data"
      }
    }
    stage('Run tasks') {
      steps {
        sh "robot Robotask.robot"
      }
    }
    stage('save') {
      steps {
step(
    [
    $class : 'RobotPublisher',
    outputPath : '/var/jenkins_home/workspace/robotest2_master/data',
    outputFileName : "*.xml",
    disableArchiveOutput : false,
    passThreshold : 100,
    unstableThreshold: 95.0,
    otherFiles : "*.png",

    ]
    )        }
    }

    stage('close') {
      steps {
        sh "rm -r data"
        sh "docker container prune --force"
      }
    }

  }
}