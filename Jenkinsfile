pipeline {
    agent {label 'SPC'}
    triggers {
        pollscm('* * * * *')
    }
    stages {
        stage('git checkout') {
            steps {
                git url: 'https://github.com/longflewtinku/spring-petclinic.git',
                    branch: 'main' 
            }
        }
        stage('build and scan') {
            steps {
             withSonarQubeEnv('SONAR') {   
                sh 'mvn package sonar:sonar'
            }
          }  
        }
    }
}