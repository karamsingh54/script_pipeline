pipeline {
    agent any

    stages {
        stage('Download data from github') {
            steps {
                git 'https://github.com/karamsingh54/jenkinstest.git'
            }
        }
    
 stages {
        stage('Transfer data') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkins1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'rsync -e ssh /var/lib/jenkins/workspace/ssh/* root@172.31.59.64:/raju', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
