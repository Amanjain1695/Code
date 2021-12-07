pipeline {
    agent {
        docker { image 'salesforce/salesforcedx:latest-full' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'sfdx version'
            }
        }
    }
}
