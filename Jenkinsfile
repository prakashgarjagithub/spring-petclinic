pipeline {
    agent { 'label JAVA_17'}
    triggers { pollSCM ('* * * * *')}
    stages {
        stage('vcs') {
            steps{
                git url: 'https://github.com/prakashgarjagithub/spring-petclinic.git'
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
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-report/TEST-*.xml'
            }
        }   
    }
}    