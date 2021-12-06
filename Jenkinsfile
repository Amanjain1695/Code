pipeline {
    agent {
        docker { image 'https://hub.docker.com/r/salesforce/salesforcedx/' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'sfdx version'
            }
        }
    }
}
