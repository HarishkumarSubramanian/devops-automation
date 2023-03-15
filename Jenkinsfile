pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/HarishkumarSubramanian/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                sh 'docker build -t harishkumar10/devops-integration .'
                }
            }
        }
        stage('Push to DokcerHub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u harishkumar10 -p ${dockerhubpwd}'
                    }
                    sh 'docker push harishkumar10/devops-integration'
                }
            }
        }
    }
}
