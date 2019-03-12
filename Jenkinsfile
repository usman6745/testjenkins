pipeline {
    agent any
    stages {
        stage ('build') {
           steps {
           //git url: 'https://github.com/usman6745/ec2-launch-jenkins.git'
           // Show the select input modal
           input message: 'Please Provide Parameters', ok: 'Next',
                        parameters: [
                        choice(name: 'key_name', choices: CPI_VPC, description: 'Available keys')]
    
           
           }
        }
   }
}   
