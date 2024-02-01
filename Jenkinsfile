#!/usr/bin/env groovy
def autoCancelled = false
pipeline {
    agent any
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 1, unit: 'SECONDS')
    }
    try {
        stages {
            stage('first-stage'){
                when { not { branch 'private/*' } }
                steps {
                    autoCancelled = true
                    error('Aborting the build.')
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
    } catch (e) {
    if (autoCancelled) {
        currentBuild.result = 'SUCCESS'
        // return here instead of throwing error to keep the build "green"
        return
    }
    // normal error handling
    throw e
    }
}