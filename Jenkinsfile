pipeline {
    agent any

    stages {
        stage('Download data from github') {
            steps {
                git branch: 'main', url: 'https://github.com/karamsingh54/jenkinstest.git'
            }
        }

        stage('Transfer data') {
            steps {
                 sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkins1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'rsync -e ssh /var/lib/jenkins/workspace/ssh/* root@172.31.59.64:/raju', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('Docker build') {
            steps {
                   sshPublisher(publishers: [sshPublisherDesc(configName: 'docker1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /tinku
                   docker build -t $JOB_NAME:v$BUILD_ID .
                   docker image tag $JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:v$BUILD_ID
                   docker image tag $JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:latest
                   docker image push karamsingh54/$JOB_NAME:v$BUILD_ID
                   docker image push karamsingh54/$JOB_NAME:latest
                   docker image rmi $JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:v$BUILD_ID karamsingh54/$JOB_NAME:latest
                    ''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

            }
        }
        stage('ansible playbook') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'docker1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /trial/ansi.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])

            }
        }

    }
    
}
    
    
    
    

    



