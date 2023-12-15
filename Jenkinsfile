pipeline {
    agent { label 'JDK_8'}
    options {
        retry(3)
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JAVA_8'
    }
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/Harika-SVL/Game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh script: 'mvn clean package'
            }
        }
        stage('report') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/target/gameoflife.war'
            }
        }
    }
}