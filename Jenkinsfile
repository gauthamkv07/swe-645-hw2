pipeline{
    agent any
    environment {
        TIMESTAMP = "${currentBuild.startTimeInMillis}"
        registryCredential = 'dockerhub'
        registry = 'kvmass/stusurvey'
    }
    stages{
        stage("Build war file") {
            steps {
                script {
                    checkout scm
                    bat 'del form.war'
                    bat 'jar -cvf form.war *'
                }
            }
        }
        stage("build docker") {
            steps {
                script {
                    dockerImageBuild = docker.build registry + ":${env.TIMESTAMP}"
                }
            }
        }
        stage("deploy docker") {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImageBuild.push()
                    }
                }
            }
        }
        stage("Deploying to  pod"){
            steps{
                bat "kubectl set image deployment/hw2-645-swe container-0=kvmass/stusurvey:${env.TIMESTAMP}"
            }
        }
    }
}