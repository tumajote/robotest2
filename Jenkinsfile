pipeline {
  agent any
  stages {
    stage('Run tasks') {
      steps {
        sh "robot --version"
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
    outputPath : '/var/jenkins_home/workspace/robotest2_master/',
    outputFileName : "*.xml",
    disableArchiveOutput : false,
    passThreshold : 100,
    unstableThreshold: 95.0,
    otherFiles : "*.png",

    ]
    )        }
    }

  }
}