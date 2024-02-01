#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 1, unit: 'SECONDS')
    }
    when { not { branch 'private/*' } }
    stages {
        stage('first-stage'){
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