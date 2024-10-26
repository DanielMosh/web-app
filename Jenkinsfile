pipeline{
    agent any

    tools {
        maven 'maven'
    }

    stages{
        stage('git clone'){
            steps{
                git branch: 'main', url: 'https://github.com/DanielMosh/web-app.git'
            }
        }
        stage('maven build package'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('code analysis'){
                environment {
                scanner = tool 'sonarq'
            }
            steps{
                script{
                   withSonarQubeEnv('sonarq'){
                       sh "${scanner}/bin/sonar-scanner -Dsonar.projectKey=dan-try-webapp"
                      }
                    }
                }
            }
        }
    }