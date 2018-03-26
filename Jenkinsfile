pipeline {
    agent any 
    parameters {
        // choices are newline separated
        string(defaultValue: "single-instance", description: 'stack name?', name: 'StackName')
        string(defaultValue: "ubuntu", description: 'key name?', name: 'KeyName')
        string(defaultValue: "t2.micro", description: 'Instance name?', name: 'InstanceType')
        choice(choices: 'US-EAST-1\nUS-WEST-2', description: 'What AWS region?', name: 'region')
        choice(choices: 'True\nFalse', description: 'Want to Describe?', name: 'Describe')
    }

    stages {
        stage('Validate') { 
            steps { 
                sh "aws cloudformation validate-template --template-body file://templates/single_instance.yml"
            }
        }
        stage('Build') { 
            steps { 
                sh "aws cloudformation create-stack --template-body file://templates/single_instance.yml --stack-name ${params.StackName} --parameters ParameterKey=KeyName,ParameterValue=${params.KeyName} ParameterKey=InstanceType,ParameterValue=${params.InstanceType}"            }
        }
        stage('Describe') {
            steps {
               //sh "aws cloudformation describe-stack-events --stack-name ${params.StackName}"
               script {
                      if ("${params.Describe}" == 'True') {
                           sh "aws cloudformation describe-stack-events --stack-name ${params.StackName}"
                      } else {
                           echo 'Will not delete'
                      }
               }
            }
       }
    }
}
