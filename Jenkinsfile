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

    stages {
        stage('Build TokensCorDapp jars') {
            steps {
                bat 'gradlew.bat clean build  prepareDockerNodes'
            }
        }
        stage('Unit & Integration Tests') {
            steps {
                bat 'gradlew.bat test integrationTest'
            }
        }
    }
}