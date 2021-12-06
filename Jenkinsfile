pipeline {
    agent {
        docker { image 'salesforce/salesforcedx:7.112.0-full' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'sfdx version'
            }
        }
    }
}
