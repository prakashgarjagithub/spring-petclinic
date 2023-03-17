pipeline {
    agent { label 'JAVA_17'}
    triggers { pollSCM ('* * * * *')}
    stages {
        stage('vcs') {
            steps{
                git url: 'https://github.com/prakashgarjagithub/spring-petclinic.git',
                    branch: 'develop'
            }
        }
        stage('build') {
            steps{
                sh './mvnw package'
            }
        }
        stage('post build') {
            steps{
                archiveArtifacts artifacts: '**/target/*.jar',
                onlyIfSuccessful: true
                junit testResults:'**/surefire-reports/TEST-*.xml'                 
            }
        }   
     }
}