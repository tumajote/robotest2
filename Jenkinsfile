pipeline {
  agent any
  stages {
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


pipeline {
  agent any
  stages {
	    stage('intialize') {
	      steps {
	        sh 'echo "PATH= ${PATH}'
	      }
	    }
    
	    stage('Run Robot Tests') {
	      steps {
		        	sh 'python3 -m robot.run --NoStatusRC --variable SERVER:${CT_SERVER} --outputdir output tasks/'
		        	sh 'exit 0'
	      		}
	      post {
        	always {
		        script {
		          step(
			            [
			              $class              : 'RobotPublisher',
			              outputPath          : 'tasks',
			              outputFileName      : '**/output.xml',
			              reportFileName      : '**/report.html',
			              logFileName         : '**/log.html',
			              disableArchiveOutput: false,
			              passThreshold       : 50,
			              unstableThreshold   : 40,
			              otherFiles          : "**/*.png,**/*.jpg",
			            ]
		          	)
		        }
	  		}		
	    }
	}    
  }
  
}
