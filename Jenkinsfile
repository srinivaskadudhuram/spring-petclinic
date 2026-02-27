pipeline {
    agent {label 'SPC'}
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git checkout') {
            steps {
                git url: 'https://github.com/srinivaskadudhuram/spring-petclinic.git',
                    branch: 'main' 
            }
        }
        stage('build and scan') {
            steps {
             withCredentials([string(credentialsId: 'sonar_id', variable: 'SONAR_TOKEN')]) {   
             withSonarQubeEnv('SONAR') {   
                sh """mvn package sonar:sonar \
                      -Dsonar.projectKey=srinivaskadudhuram_spring-petclinic-srinu \
                      -Dsonar.organization=srinivaskadudhuram \
                      -Dsonar.host.url=https://sonarcloud.io/ \
                      -Dsonar.login=$SONAR_TOKEN""" 
            }

          }  
        }
     }  
    }
}