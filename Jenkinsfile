/**
 * Tracking if the build was aborted
 */
Boolean buildAborted = false
/**
 * Abort the build with a message
*/
// check if the branch name starts with 'private/' and skip the build if it does
if (env.BRANCH_NAME ==~ /^private\//) {
    echo "NetBox private/* branches are not built by default."
    currentBuild.result = 'SUCCESS'
    return
}

pipeline {
    agent any
    stages {
        stage('One') {
            // when { not { branch 'private/*' } }
            steps {
                script {
                    // buildAborted = true
                    // currentBuild.result = 'SUCCESS'
                    // return
                    echo 'Doing stage 1'
                }
                // script {
                //     try {
                //         echo 'Doing stage 1'
                //         if(params.FailOrAbort == 'fail') {
                //             echo "This build will fail"
                //             error("Build has failed")
                //         }
                //         else if(params.FailOrAbort == 'abort') {
                //             echo "This build will abort with SUCCESS status"
                //             abortBuild("This build was aborted")
                //         }
                //         else {
                //             echo "This build is a success"
                //         }
                //         echo "Stage one steps..."
                //     }
                //     catch(e) {
                //         echo "Error in Stage 1: ${e.getMessage()}"
                //         if(buildAborted) {
                //             echo "It was aborted, ignoring error status"
                //         }
                //         else {
                //             error(e.getMessage())
                //         }
                //     }
                // }
            }
            post {
                always {
                    echo "Stage 1 failed"
                }
            }
        }
        stage('Two') {
            when {
                expression {
                    return !buildAborted
                }
            }
            steps {
                echo "Doing stage 2"
            }
        }
        stage('Three') {
            when {
                expression {
                    return !buildAborted
                }
            }
            steps {
                echo "Doing stage 3"
            }
        }
    }
    post {
        always  {
            echo "Build completed. currentBuild.result = ${currentBuild.result}"
        }
        // success {
        //     script {
        //         if(buildAborted) {
        //             echo "Build was aborted"
        //         } else {
        //             echo 'Build was a complete success'
        //         }
        //     }
        // }
        // unstable {
        //     echo 'Build has gone unstable'
        // }
    }
}
