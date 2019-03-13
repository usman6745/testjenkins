pipeline {
  agent any
  parameters {
    string(description: 'enter ami_id', name: 'ami_id')
    string(description: 'enter Instance Type', name: 'Instance_type')
    string(description: 'enter subnet id', name: 'subnetid')
    string(description: 'enter region name', name: 'region_name')
    string(description: 'enter Key name', name: 'Key_Name')
    string(description: 'enter Key-value-name', name: 'Key_Name_Value')
    choice(choices: ['CI_VPC', 'test1'], description: 'choose key pair?', name: 'keypair_name')
  }

  stages {

    stage('build') {
      steps {
        withCredentials([[
          $class: 'AmazonWebServicesCredentialsBinding',
          credentialsId: 'aws-access',
          accessKeyVariable: 'AWS_ACCESS_KEY_ID',
          secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
        ]]) {
          git url: 'https://github.com/usman6745/jenkins-aws-ec2-launch.git'
          sh '''
          chmod +x ec2.sh
            ./ec2.sh $ami_id $keypair_name $Instance_type $subnetid $region_name $Key_Name $Key_Name_Value
        ''' 
          instanceid-value = sh (
            echo "$Key_Name_Value"
            //script: "aws ec2 describe-instances --filters "Name=tag:"${Key_Name}",Values="${Key_Name_Value}"" | grep '\\[InstanceId]'",
          returnStatus: true
          ) == 0
          echo "InstanceID is : ${instanceid-value}"
          //sh '''
          //aws ec2 describe-instances --filters "Name=tag:name,Values=web1" > Instance-ID_VALUE
          //cat Instance-ID_VALUE
          //'''
          
          // Show the select input modal
          //echo "${ ami_id }"
          //echo "${key_name}"
         

        }
        //          withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-access', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        // some block



      }
    }
    stage('slacknotification') {
      steps{      
      slackSend baseUrl: 'https://opstree.slack.com/services/hooks/jenkins-ci/',
      channel: 'ot-meesho',
      color: 'good',
        message: 'Jenkins-Slack Intigrated',
      //message: 'Instance has launched',
      //message: ' $LaunchInstanceID ',
      teamDomain: 'opstree',
      tokenCredentialId: 'slack-token'
    }
  }
}
}
