pipeline {
    agent any 
    parameters {
        string(defaultValue: "TEST", description: 'What environment?', name: 'userFlag')
        // choices are newline separated
        choice(choices: 'US-EAST-1\nUS-WEST-2', description: 'What AWS region?', name: 'region')
    }

    stages {
        stage('Validate') { 
            steps { 
                sh 'aws cloudformation validate-template --template-body file://templates/single_instance.yml' 
            }
        }
        stage('Build') { 
            steps { 
                sh 'aws cloudformation create-stack --template-body file://templates/single_instance.yml --stack-name single-instance --parameters ParameterKey=KeyName,ParameterValue=tutorial ParameterKey=InstanceType,ParameterValue=t2.micro' 
            }
        }
        stage('Describe') {
            steps {
               sh 'aws cloudformation describe-stack-events --stack-name single-instance' 
            }
       }
    }
}
