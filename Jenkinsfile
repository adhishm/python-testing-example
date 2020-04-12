stage('CI') {
    node('master') {
        try {
            checkout scm
            // git repo and branch defined inside Jenkins job
            
            sh label: '',
                script: 'python -m unittest test_calc'
            
            notify('Success')
        } catch(err) {
            notify("Build failed: ${err}")
            currentBuild.result = 'FAILURE'
        }
    }
}

def notify(status){
    emailext (
        from: "jenkins-server@secret.garden",
        to: "adhishm@gmail.com",
        subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
        body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
