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
    
stage('Rename Package'){
steps {
sh 'mv ${WORKSPACE}/target/mylab-1.0-SNAPSHOT.war ${WORKSPACE}/target/myjava.war'
}
}
    
stage('Validation'){
steps {
input 'Kindly Approve This Package'
}
}
    
stage('Deployment'){
steps {
sshPublisher(publishers: [sshPublisherDesc(configName: 'SSH_SERVER', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/target/', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
}
}  
    
stage('Eamil'){
post { always {
script {
def jobName = env.JOB_NAME
def buildNumber = env.BUILD_NUMBER
def pipelineStatus = currentBuild.result ?: 'UNKNOWN'
def bannerColor = pipelineStatus.toUpperCase() == 'SUCCESS' ? 'green' : 'red'
def body = """
echo '<html>'
echo '<body>'
echo '<div style="border: 4px solid ${bannerColor}; padding:10px;">'
echo '<h2>${jobName} - Build ${buildNumber}</h2>'
echo '<div style="background-color: ${bannerColor}; padding:
echo '<h3 style="color: white;">Pipeline Status:${pipelineStatus.toUpperCase()}</h3>'
echo '<p>Check the <a href="${BUILD_URL}">console output</a>.</p>'
"""
echo '</div>'
echo '</body>'
echo '</html>'
emailext (
subject: "${jobName} - Build ${buildNumber} - ${pipelineStatus.toUpperCase()}", body: body,
to: 'amoolekan@outlook.com', from: 'jenkins@example.com', replyTo: 'jenkins@example.com', mimeType: 'text/html', attachmentsPattern: 'trivy-image-report.html'
)
}
}
}
)
    
}
    
}
//
