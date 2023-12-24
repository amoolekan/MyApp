pipeline {
    agent any
    
    tools {
        maven 'MVN'
    }
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts 3'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
                stage ("Deploy to Staging"){
                    steps {
                        sh 'echo clean build'
                    }
                }
            
        }
    }
}
