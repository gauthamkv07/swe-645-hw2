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
                    del form.war
                    'jar -cvf form.war *'
                    'docker login -u kvmass -p Herndon@123'
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
    }
}