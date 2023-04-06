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
    }
    // stages {
    //     stage("Build the image") {
    //         steps {
    //             script {
    //                 checkout scm
    //                 sh 'rm -rf *.war'
    //                 sh 'jar -cvf form.war *'
    //                 sh 'echo $(BUILD_TIMESTAMP)'
    //                 sh 'docker login -u kvmass ${DOCKERHUB_PASSWORD}'
    //                 def customImage = docker.build{'kvmass/stusurvey'}
    //             }
    //         }
    //     }
    //     stage("Pushing Image to DockerHub"){
    //         steps {
    //             script {
    //                 sh 'docker push kvmass/stusurvey'
    //             }
    //         }
    //     }
        // stage("Deploying to Rancher"){
        //     steps {
        //         script {
        //             sh 'kubectl set image deployment/pipeline stusurvey-pipeline=kvmass/stusurvey:${BUILD_TIMESTAMP} -n jenkins-pipeline'
        //         }
        //     }
        // }
        // stage("Deploying to Rancher as with load balancer"){
        //     steps {
        //         script {
        //             sh 'kubectl set image deployment/pipeline stusurvey-pipeline=kvmass/stusurvey:${BUILD_TIMESTAMP} -n jenkins-pipeline'
        //         }
        //     }
        // }
    // }
}