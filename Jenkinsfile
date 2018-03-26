pipeline {
    agent any 

    stages {
        stage('Build') { 
            steps { 
                sh 'aws cloudformation create-stack --template-body file://templates/single_instance.yml --stack-name single-instance --parameters ParameterKey=KeyName,ParameterValue=tutorial ParameterKey=InstanceType,ParameterValue=t2.micro' 
            }
        }
        stage('NexusArtifactUploaderJob') {
            steps {
               sh 'ls' 
            }
       }
    }
}
