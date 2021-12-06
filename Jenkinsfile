pipeline {
    agent {
        docker {
            image 'curlybracket/salesforce:latest'
        }
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
