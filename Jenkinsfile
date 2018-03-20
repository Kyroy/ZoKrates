#!/usr/bin/env groovy

pipeline {
    agent { docker 'kyroy/zokrates-base-test' }
    stages {
//        stage('Clippy') {
//            steps {
//                sh "cargo +nightly clippy --all"
//            }
//        }
//        stage('Rustfmt') {
//            steps {
//                // The build will fail if rustfmt thinks any changes are
//                // required.
//                sh "cargo +nightly fmt --all -- --write-mode diff"
//            }
//        }

        stage('Build') {
            steps {
                sh 'cargo build --release'
            }
        }

        stage('Test') {
            steps {
                sh 'cargo test'
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
