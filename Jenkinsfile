node ('master') {
    try {
        stage('import'){
            try{
                dir('task-tracker') {
                    git url:'https://github.com/paul-mcinnis/task-tracker.git'
                }   
            } catch(err) {
                currentBuild.result = 'ABORTED'
                error("IMPORT")
            }
        }

        stage('export'){
                    try{
                        dir('task-tracker') {
                            // git checkout master
                            // git commit -am "Build number ${env.BUILD_NUMBER}"
                            git push origin master
                        }
                    } catch(err) {
                        currentBuild.result = 'ABORTED'
                        error("EXPORT")
                    }
                }
    } catch(err) {
        // slackSend color: "danger", message: "Error: ${err.message} stage failure: ${env.BUILD_NUMBER}"
    }
}
