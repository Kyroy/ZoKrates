#!/usr/bin/env groovy

pipeline {
    agent { docker 'zokrates-base' }
    stages {
        stage('Init') {
            steps {
                echo 'init'
            }
        }

        stage('Lint') {
            steps {
                echo 'lint'
            }
        }

        stage('Test') {
            steps {
                echo 'test'
//                archive "*.xml"
//
//                step([$class             : 'CoberturaPublisher',
//                      autoUpdateHealth   : false,
//                      autoUpdateStability: false,
//                      coberturaReportFile: coverXML,
//                      failUnhealthy      : false,
//                      failUnstable       : false,
//                      maxNumberOfBuilds  : 0,
//                      onlyStable         : false,
//                      sourceEncoding     : 'ASCII',
//                      zoomCoverageChart  : false])
            }
        }
    }
    post {
        always {
            junit allowEmptyResults: true, testResults: '*test.xml'
            deleteDir()
        }
    }
}
