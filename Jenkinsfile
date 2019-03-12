pipeline {
    agent any
    parameters {
        string (description: 'enter ami_id', name: 'ami_id')
        choice (choices: ['CI_VPC', 'test1'], description: 'choose key pair?', name: 'key_name')
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
           git url: 'https://github.com/usman6745/ec2-launch-jenkins.git'
           sh '''
                 chmod +x ec2.sh
                 ./ec2.sh
           '''
               // Show the select input modal
               //echo "${ ami_id }"
               //echo "${key_name}"
               
            sh '''
            echo ${AWS_ACCESS_KEY_ID}
            '''
            }
//          withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-access', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
   // some block

        }         
           }
        }
   }

