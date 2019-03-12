pipeline {
    agent any
    stages {
        stage ('build') {
           steps {
           //git url: 'https://github.com/usman6745/ec2-launch-jenkins.git'
           // Show the select input modal
           input "do you want proceed"
            echo "hello from stage two"
               parameters {
                   string (description:'enter ami_id', name: 'ami_id')
               }
               echo $amid_id
    
           
           }
        }
   }
}   
