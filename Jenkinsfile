node ('master') {
    def success = false
    try {
        stage('import'){
            try{
                dir('task-tracker') {
                    sh("rm -rf task-tracker")
                    sh("git clone https://github.com/paul-mcinnis/task-tracker")
                }
            } catch(err) {
                currentBuild.result = 'ABORTED'
                error("IMPORT")
            }
        }

        stage('export'){
                    try{
                        dir('task-tracker') {
                            sshagent (credentials: ['87fac123-1144-4b20-a928-aaa8480c3db5']) {
                                sh('(cd task-tracker && git checkout dev && git push origin master)')
                            }
                        }
                    } catch(err) {
                        currentBuild.result = 'ABORTED'
                        error("EXPORT")
                    }
                }
        success = true
    } catch(err) {
        // slackSend color: "danger", message: "Error: ${err.message} stage failure: ${env.BUILD_NUMBER}"
    } finally {
            if(success == true) {
                // slackSend color: "good", message: "Build ${env.BUILD_NUMBER} successfully DEPLOYED"
            } else {
                currentBuild.result = "FAILURE"
            }
    }
}
