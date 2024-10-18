pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // Poll every minute, adjust as necessary
    }
    stages {
        stage('Snyk Open Source Scan') {
            when {
                anyOf {
                    branch 'main'
                    branch 'master'
                }
            }
            steps {
                script {
                    sh 'snyk test --all-projects'
                }
            }
        }
        stage('Snyk Code Scan') {
            when {
                anyOf {
                    branch 'main'
                    branch 'master'
                }
            }
            steps {
                script {
                    sh 'snyk code test'
                }
            }
        }
    }
    post {
        always {
            junit '**/TEST-*.xml'
        }
    }
}
