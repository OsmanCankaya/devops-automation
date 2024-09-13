pipeline{
    agent any
    tools{
        maven "maven_3_9_8"
    }
    stages{
        stage("Build Maven"){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/OsmanCankaya/devops-automation']])
                bat "mvn clean install"
            }
        }
        stage("Build Docker Image"){
            steps{
                bat "docker build -t osmancankaya/devops-integration ."
            }
        }
        stage("Push Image To hub"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        bat "docker login -u osmancankaya -p ${dockerhubpwd}"
                    }
                    bat "docker push osmancankaya/devops-integration"
                }
            }
        }
    }

}