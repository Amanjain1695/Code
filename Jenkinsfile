pipeline {
    agent {
        docker { image 'salesforce/salesforcedx:latest-rc-slim' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
