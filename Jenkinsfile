pipeline {
    agent {
        docker { image 'salesforce/salesforcedx:latest-slim' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'sfdx version'
            }
        }
    }
}
