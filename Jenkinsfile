/* This is a simple Jenkins pipeline created by Karam singh */

pipeline {
    agent any
    stages {
        stage('First step of pipeline is to Download data from github') {
            steps {
                git branch: 'main', url: 'https://github.com/karamsingh54/jenkinstest.git'
            }
        }

        stage('Transfer data from Jenkins server to docker-ansible server using publish over ssh') {
            steps {
                 sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkins1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'rsync -e ssh /var/lib/jenkins/workspace/devops_pipeline/Dockerfile* root@172.31.59.64:/trial', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('Building docker image from Dockerfile,removing old version of docker image and pushing it on dockerhub account') {
            steps {
                   sshPublisher(publishers: [sshPublisherDesc(configName: 'docker1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /trial
                   docker build -t $JOB_NAME:v$BUILD_ID .
                   docker image tag $JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:v$BUILD_ID
                   docker image tag $JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:latest
                   docker image push karamsingh54/$JOB_NAME:v$BUILD_ID
                   docker image push karamsingh54/$JOB_NAME:latest
                   docker image rmi $JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:latest
                    ''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

            }
        }
        stage('ansible playbook for creating the final web container on webnode') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'docker1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /trial/ansi.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

            }
        }

    }
    
}
    
    
    
    

    



