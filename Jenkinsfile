#!/usr/bin/env groovy

pipeline {
    agent any
    stages {
        withDockerContainer('kyroy/zokrates-base-test') {
            stage('Build & Test') {
                steps {
                    sh 'RUSTFLAGS="-D warnings" cargo build --release'
                    sh 'RUSTFLAGS="-D warnings" cargo test'
                }
            }
        }

        stage('Docker Build & Push') {
            when {
                environment name: 'BRANCH_NAME', value: 'master'
                // expression { env.BRANCH_NAME == "master" }
            }
            steps {
                script {
                    def dockerImage = docker.build("kyroy/zokrates")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-kyroy') {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
    post {
        always {
            // junit allowEmptyResults: true, testResults: '*test.xml'
            deleteDir()
        }
    }
}
