pipeline {
    agent any 

    stages {
        stage('Build') { 
            environment {
                 JAVA_HOME = tool 'jdk-8u45'
                 PATH="${JAVA_HOME}/bin:${PATH}"
                 MAVEN_HOME = tool 'M3'
            }
            steps { 
                sh 'aws cloudformation create-stack --template-body file://templates/single_instance.yml --stack-name single-instance --parameters ParameterKey=KeyName,ParameterValue=tutorial ParameterKey=InstanceType,ParameterValue=t2.micro' 
            }
        }
        stage('NexusArtifactUploaderJob') {
            steps {
              nexusArtifactUploader artifacts: [[artifactId: 'nexus-artifact-uploader', classifier: 'debug', file: 'nexus-artifact-uploader.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'sd.sd', nexusUrl: '172.17.0.2:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '2'
            }
       }
    }
}
