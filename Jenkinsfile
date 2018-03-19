#!/usr/bin/env groovy

pipeline {
    agent { docker 'kyroy/zokrates-base-test' }
    stages {
        stage('Init') {
            steps {
                echo 'init'
            }
        }

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

//        stage('Build') {
//            steps {
//                sh 'cargo build --release'
//            }
//        }

//        stage('kcov') {
//            steps {
//                sh 'cargo kcov -v'
//                archive "**/*.xml"
//            }
//        }

        stage('Test') {
            steps {
//                sh 'cargo test'
                sh 'cargo test-junit --name cargo_test.xml'
                archive "**/*.xml"
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
            sh 'find . -name "*.xml"'
            archive "**/*.xml"
            junit allowEmptyResults: true, testResults: '*test.xml'
            deleteDir()
        }
    }
}
