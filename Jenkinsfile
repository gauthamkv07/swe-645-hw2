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
                    dockerImageBuild = docker.build registry + ${currentBuild.startTimeInMillis}
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