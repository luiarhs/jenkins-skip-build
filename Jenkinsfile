#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 1, unit: 'SECONDS')
    }
    stages {
        stage('first-stage'){
            when { not { branch 'private/*' } }
            steps {
                echo 'Skipped full build.'
            }
        }
        stage('second-stage') {
            when {
                not {
                    branch 'release/*'
                }
                not {
                    branch 'staging'
                }
            }
            steps{
                echo 'second full build.'
            }
        }
    }
}