#!groovy
/**
 * Jenkins pipeline to build the kotlin CorDapp template
 */

/**
 * Kill already started job.
 * Assume new commit takes precedence and results from previousunfinished builds are not required.
 * This feature doesn't play well with disableConcurrentBuilds() option
 */

pipeline {
    agent any

    environment {
        JENKINS_UID = sh(returnStdout: true, script: "id -u ${USER}").trim()
    }
    stages {
        stage('Build Tokens CorDapp ') {
            steps {
                sh 'cp nodeConfigFiles/buildDockerNodes.gradle .'
                sh 'mv "buildDockerNodes.gradle" "build.gradle"'
                sh './gradlew prepareDockerNodes'
            }
        }
        stage('Apply Configuration') {
            steps {
                sh 'bash -c "chown -R ${JENKINS_UID} /build"'
                sh 'cp "nodeConfigFiles/Diahnne Abbott.config" .'
                sh 'cp "nodeConfigFiles/Peter Boyle.config" .'
                sh 'cp "nodeConfigFiles/Robert Anthony.config" .'
                sh 'cp "nodeConfigFiles/NetworkMap.config" .'
                sh 'cp "nodeConfigFiles/Notary.config" .'
                sh 'cp "nodeConfigFiles/Oracle.config" .'
                sh 'mv "Diahnne Abbott.config" "build/nodes/DiahnneAbbott/node.conf"'
                sh 'mv "Peter Boyle.config" "build/nodes/PeterBoyle/node.conf"'
                sh 'mv "Robert Anthony.config" "build/nodes/RobertAnthony/node.conf"'
                sh 'mv "NetworkMap.config" "build/nodes/NetworkMap/node.conf"'
                sh 'mv "Notary.config" "build/nodes/Notary/node.conf"'
                sh 'mv "Oracle.config" "build/nodes/Oracle/node.conf"'


            }
        }
        stage('Run Unit & Integration Tests') {
            steps {
                sh './gradlew test integrationTest'
            }
        }
    }

    post {
        aborted {
            error "Aborted, exiting now"
        }
        failure {
            error "Failed, exiting now"
        }
    }
}