pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                gerritReview labels: [Verified: 0]
                echo 'Hello World !!!'
            }
        }
    }
    post {
        success {
            gerritReview labels: [Verified: 1]
            gerritCheck checks: ['example:checker': 'SUCCESSFUL']
        }
        unstable { gerritReview labels: [Verified: 0], message: 'Build is unstable' }
        failure {
            gerritReview labels: [Verified: -1]
            gerritCheck checks: ['example:checker': 'FAILED'], message: 'invalid syntax'
        }
    }
}
