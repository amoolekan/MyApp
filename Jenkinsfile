pipeline {
agent any
    
options {
 durabilityHint 'MAX_SURVIVABILITY'
}

tools {
maven 'MVN'
}
    
stages{

stage('CodeAnalysis'){
steps {
withSonarQubeEnv(installationName: 'Sonarqube') {
sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
}
}
}
    
//stage('Compile'){
//steps {
//sh 'mvn clean'
//sh 'mvn compile'
//}
//}

//stage('Test'){
//steps {
//sh 'mvn test'
//}
//}

//stage('Build'){
//steps {
//sh 'mvn package'
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
    
//stage('Validation'){
//steps {
//input 'Kindly Approve This Package'
//}
//}
    
//stage('Deployment'){
//steps {
//sshPublisher(publishers: [sshPublisherDesc(configName: 'SSH_SERVER', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/target/', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
//}
//}  

stage('Email Notification'){
steps {
sh 'echo Sending email'
}
    
post {
    
always {
emailext (
subject: '$DEFAULT_SUBJECT',
to: '$DEFAULT_RECIPIENTS',
body: '$DEFAULT_CONTENT', 
attachLog: 'true',
recipientProviders: [ requestor() ]
)
}
    
//success {
//emailext (
//subject: '$DEFAULT_SUBJECT',
//to: '$DEFAULT_RECIPIENTS',
//body: '$DEFAULT_CONTENT', 
//attachLog: 'true',
//recipientProviders: [ requestor() ]
//)
//}

//failure {
//emailext (
//subject: '$DEFAULT_SUBJECT',
//to: '$DEFAULT_RECIPIENTS',
//body: '$DEFAULT_CONTENT', 
//attachLog: 'true',
//recipientProviders: [ requestor() ]
//)
//}
    
//unstable {
//emailext (
//subject: '$DEFAULT_SUBJECT',
//to: '$DEFAULT_RECIPIENTS',
//body: '$DEFAULT_CONTENT', 
//attachLog: 'true',
//recipientProviders: [ requestor() ]
//)
//}
    
}    
}
    
}    
}


