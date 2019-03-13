pipeline {
    agent any
    parameters {
        string (description: 'enter ami_id', name: 'ami_id')
        string (description: 'enter Instance Type', name: 'Instance_type')
        string (description: 'enter subnet id', name: 'subnetid')
        string (description: 'enter region name', name: 'region_name')
        choice (choices: ['CI_VPC', 'test1'], description: 'choose key pair?', name: 'keypair_name')
    }
    
    stages {
        
        stage ('build') {
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
                 ./ec2.sh $ami_id $keypair_name $Instance_type $subnetid $region_name
           '''
               // Show the select input modal
               //echo "${ ami_id }"
               //echo "${key_name}"
               
            }
//          withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-access', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
   // some block
               
               

        }         
           }
        
   }
}
