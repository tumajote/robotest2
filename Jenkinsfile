pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        sh "mkdir data"
      }
    }
    stage('build and run') {
      steps {
        sh "docker run --rm \
        -v /var/jenkins_home/workspace/robotest_master/data:/opt/robotframework/reports:Z \
        -v /var/jenkins_home/workspace/robotest_master/tasks:/opt/robotframework/tests:Z \
        ppodgorsek/robot-framework"
      }
    }
    stage('save') {
      steps {
step(
    [
    $class : 'RobotPublisher',
    outputPath : '/var/jenkins_home/workspace/robotest_master/data',
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