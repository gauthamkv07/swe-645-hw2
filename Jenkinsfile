pipeline{
    agent any
    environment {
        registryCredential = 'dockerhub'
        registry = 'kvmass/stusurvey'
        DATE_TAG = java.time.LocalDate.now()
    }
    stages{
        stage("Build the image") {
            steps {
                script {
                    checkout scm
                    bat 'del form.war'
                    bat 'jar -cvf form.war *'
                    bat 'docker login -u kvmass -p Herndon@123'
                    bat "echo ${DATETIME_TAG}"
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
                bat "kubectl set image deployment/hw2-645-swe container-0=kvmass/stusurvey:$lates"
            }
        }
    }
}