pipeline{
  agent{
    label { label 'itcloudconfig' 
    }
  }
  stages {
      stage ('startERPDatabase'){
      steps{
           //sh 'sleep 30s'
           echo 'Stopping the Application Services' 
           sh 'sudo cat /etc/redhat-release > release.txt'
           //sh 'sudo su bramireddy /home/bramireddy/space.sh '
           sh  'ls -ltr'
           sh 'pwd > present.txt'
      }
      }
      stage ('startERPApplication'){
      steps{
           echo 'stopping the Database' 
           //sh 'sleep 10s'
           //sh 'exit 1'
      }
  }
    stage ('SanityCheck'){
      steps{
           echo 'Patching the Database Server'
           //sh 'sudo yum update --security --assumeno'
           //sh 'sleep 120s'
           sh '/home/jenkins/patchlog.sh'
           //sh 'nohup sudo reboot &>/dev/null & exit'
      }
    }
    stage ('NexposeScan'){
      steps{
          echo 'Scan Kickoff'
      }
    }
  }
  post {
    success {
                echo 'Patching Completed'
           mail to: 'bramireddy@idirect.net',
             subject: "Started  Services : ${currentBuild.fullDisplayName}",
             body: "Patching Completed on ERP Application  ${env.BUILD_URL}/consoleText"
    }
     failure {
               echo 'Failed'
           mail to: 'bramireddy@idirect.net',
             subject: " Services Failed to start the application : ${currentBuild.fullDisplayName}",
             body: "Services Failed to Start on ERP Application  ${env.BUILD_URL}/consoleText"
    }
  }
}
