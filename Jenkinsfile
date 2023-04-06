pipeline{
    agent any
    environment {
        registryCredential = 'dockercred'
        registry = 'kvmass/stusurvey'
    }
    stages{
        stage("Build the image") {
            steps {
                script {
                    checkout scm
                    'del form.war'
                    'jar -cvf form.war *'
                }
            }
        }
        stage("build docker") {
            steps {
                script {
                    'docker build -t kvmass/stusurvey .'
                }
            }
        }
        stage("push docker image") {
            steps {
                script {
                    'docker push kvmass/stusurvey'
                }
            }
        }
    }
}