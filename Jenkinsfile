pipeline{
  agent{
    label { label 'itcloudconfig' 
    }
  }
  stages {
      stage ('stopERPDatabase'){
      steps{
           echo 'Stopping the Application Services' 
           sh 'sudo cat /etc/redhat-release > release.txt'
           sh 'sudo su bramireddy /home/bramireddy/space.sh '
           sh  'ls -ltr'
           sh 'pwd > present.txt'
      }
      }
      stage ('stopERPApplication'){
      steps{
           echo 'stopping the Database' 
           //sh 'sleep 10s'
           //sh 'exit 1'
      }
  }
    stage ('Sanity Check'){
      steps{
           echo 'Patching the Database Server'
           //sh 'sudo yum update --security --assumeno'
           //sh 'sleep 120s'
           sh 'sudo cat  /var/log/yum.log'
           //sh 'nohup sudo reboot &>/dev/null & exit'
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
        mail to: 'bramireddy@idirect.net',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Services  Failed for some reason  ${env.BUILD_URL}/consoleText"
    }
  }
}
