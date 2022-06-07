pipeline {
    agent { label 'jdk8'}
    options { 
        timeout(time: 1, unit: 'HOURS')
        retry(2)
        }
        triggers {
        cron('H * * * *')
    }
    parameters { 
        choice(name: 'CHOICES', choices: ['compile', 'package', 'clean package']) 
        }
    stages {
        stage('SourceCode') {
            steps {
                git branch: 'master', 
                url: 'https://github.com/penumallipurna/game-of-life.git'
            }
        }
        stage('Build and sonarqube-analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                 sh "mvn ${params.CHOICES} sonar:sonar"
              }
                
            }
        }
        stage('Test Results') {
            steps {
               junit testResults:'**/surefire-reports/*.xml'
              
            }
        }
    }
}