pipeline {
agent any

tools {
maven 'MVN'
}
    
stages{
    
//stage('Build'){
//steps {
//sh 'mvn clean test package'
//sh 'mvn clean package'
//sh 'echo Clean build completed'
//}
//post {
//success {
//echo 'Archiving the artifacts 3'
//archiveArtifacts artifacts: '**/target/*.war'
                    
//}
//}
//}
    
//stage('Rename Package'){
//steps {
//sh 'mv ${WORKSPACE}/target/mylab-1.0-SNAPSHOT.war ${WORKSPACE}/target/myjava.war'
//}
//}
    
stage('Validation'){
steps {
input 'Kindly Approve This Package'
}
}
    
//stage('Deployment'){
//steps {
//sshPublisher(publishers: [sshPublisherDesc(configName: 'SSH_SERVER', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/target/', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
//}
//}  

stage('Email'){
steps {
    sh 'echo Sending email'
}
 post {
        always {
            emailext (
          subject: '$DEFAULT_SUBJECT',
          body: '$DEFAULT_CONTENT',
          to: '$DEFAULT_RECIPIENTS',
          recipientProviders: [ requestor() ]
        )
        }
    }
}
    
}    
}

//
