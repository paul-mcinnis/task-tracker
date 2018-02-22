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
    } catch(err) {
        // slackSend color: "danger", message: "Error: ${err.message} stage failure: ${env.BUILD_NUMBER}"
    }
}
