#!groovy

properties([
        disableConcurrentBuilds(),
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '2')),
])

node('master') {
    stage('Prepare') {
        deleteDir()
        checkout scm
    }

    stage('Generate') {
        withEnv([
                "PATH+MVN=${tool 'mvn'}/bin",
                "JAVA_HOME=${tool 'jdk8'}",
                "PATH+JAVA=${tool 'jdk8'}/bin"
        ]) {
            sh 'mvn -e clean verify'
        }
    }

    stage('Archive Test Report') {
        archive 'target/surefire-reports/*-output.txt'
    }
}