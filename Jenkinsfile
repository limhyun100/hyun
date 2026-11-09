pipeline {
    agent any
    tools { nodejs 'nodejs' }

        stage('Run Postman Collections') {
            steps {
                bat 'newman run Login_API_Test.postman_collection.json -e GameQA_ENV.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export newman/Login_Report.html --export-environment GameQA_ENV.postman_environment.json'
                bat 'newman run Ranking_API_Test.postman_collection.json -e GameQA_ENV.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export newman/Ranking_Report.html'
                bat 'newman run Item_Grant_API_Test.postman_collection.json -e GameQA_ENV.postman_environment.json -r cli,htmlextra --reporter-htmlextra-export newman/ItemGrant_Report.html'
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
