pipeline {
    agent any
    tools { nodejs 'nodejs' }
    stages {
        stage('Run Postman Collections') {
    steps {
        bat 'echo JENKINS_BAT_OK'
        bat 'call run_all_tests.bat'
    }
}
    }

    post {
        always {
            archiveArtifacts artifacts: 'newman/*.html', fingerprint: true
            publishHTML(target: [
                reportDir: 'newman',
                reportFiles: 'Login_Report.html,Ranking_Report.html,ItemGrant_Report.html',
                reportName: 'Newman Reports',
                keepAll: true,
                alwaysLinkToLastBuild: true
            ])
        }
    }
}
