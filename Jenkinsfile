pipeline {
    agent any
    
    tools {
        maven 'MVN'
    }
stages{
        stage('Build'){
            steps {
                sh 'mvn clean test package'
                sh 'echo Clean build completed'
            }
            post {
                success {
                    echo 'Archiving the artifacts 3'
                    archiveArtifacts artifacts: '**/target/*.war'
                    
                }
            }
        }
     stage('Validation'){
            steps {
                input 'Kindly Validate This Package'
            }
     }
    stage('Deployment'){
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'SSH_SERVER', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/target/', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
            }
        }
}
}
