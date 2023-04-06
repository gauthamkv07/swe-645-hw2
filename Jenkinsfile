pipeline{
    agent any
    environment {
        registryCredential = 'dockerhub'
        registry = 'kvmass/stusurvey'
    }
    stages{
        stage("Build the image") {
            steps {
                script {
                    checkout scm
                    bat 'del form.war'
                    bat 'jar -cvf form.war *'
                    bat 'docker login -u kvmass -p Herndon@123'
                }
            }
        }
        stage("build docker") {
            steps {
                script {
                    dockerImageBuild = docker.build registry + ":latest"
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
        stage("Deploying to first pod"){
            steps{
                bat "kubectl set image deployment/hw2-645-swe hw2-645-swe-b758fbf4-2p4dc=kvmass/stusurvey:latest"
            }
        }
    }
}