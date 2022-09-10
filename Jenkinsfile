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
        stage('Gradle') {
            steps {
                bat 'gradlew.bat clean build test prepareDockerNodes'
            }
        }
    }
}