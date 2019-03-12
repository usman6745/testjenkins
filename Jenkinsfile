pipeline {
    agent any
    parameters {
        string (description: 'enter ami_id', name: 'ami_id')
        choice (choices: ['CI_VPC', 'test1'], description: 'choose key pair?', name: 'key_name')
    }
    stages {
        stage ('build') {
           steps {
           git url: 'https://github.com/usman6745/ec2-launch-jenkins.git'
           chmod +x ec2.sh
           sh ./ec2.sh    
               // Show the select input modal
               //echo "${ ami_id }"
               //echo "${key_name}"
    
           
           }
        }
   }
}   
