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
                    echo "TimeStamp: ${currentBuild.startTimeInMillis}"
                }
            }
        }
        stage("build docker") {
            steps {
                script {
                    'docker build -t kvmass/stusurvey .'
                    'docker tag kvmass/stusurvey:${currentBuild.startTimeInMillis}'
                }
            }
        }
        stage("push docker image") {
            steps {
                script {
                    'docker push kvmass/stusurvey:${currentBuild.startTimeInMillis}'
                }
            }
        }
    }
}