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
        stage('upload to nexus'){
            steps{
                nexusArtifactUploader artifacts: 
                    [[artifactId: 'maven-web-application',
                    classifier: '',
                    file: '/var/lib/jenkins/workspace/jenkinsfile_another_try/target/web-app.war',
                    type: 'war']],
                    credentialsId: 'usr.name_usr.pass',
                    groupId: 'com.mt',
                    nexusUrl: '35.92.24.113:8081/repository/another-repo/',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'another-repo',
                    version: '3.8.1-Release'
            }
        }
    }
}