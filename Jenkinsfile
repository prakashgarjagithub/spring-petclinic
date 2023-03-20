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
        stage('sonarcloud') {
            steps{
                sh 'mvn clean verify sonar:sonar \
                -Dsonar.login=afafbaeafe9e0838af126c5d3e1a93e08f9de8f9 \
                -Dsonar.host.url=https://sonarcloud.io \
                -Dsonar.organization=prakashgarjagithub \
                -Dsonar.projectKey=prakashgarjagithub'
            }
        }
        stage('upload s3 bucket') {
            steps{
                sh 'aws s3 cp /home/ubuntu/remote/workspace/spc_develop/target/spring-petclinic-3.0.0-SNAPSHOT.jar s3://qt4362'
            }
        }        
    }
}    