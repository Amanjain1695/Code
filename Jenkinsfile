pipeline {
    agent {
        docker {
            image 'curlybracket/salesforce:latest'
        }
    }
    stage('Add other packages') {
    echo "Installing A"
    timeout(900) {
        waitUntil {
            sh "sfdx force:package:install --package --wait 15"
        }
    }
    echo "A installed"
    environment {
        SF_CONSUMER_KEY='env.CONNECTED_APP_CONSUMER_KEY_DH'
    SF_USERNAME='env.HUB_ORG_DH'
     SERVER_KEY_CREDENTALS_ID='env.JWT_CRED_ID_DH'
     TEST_LEVEL='RunLocalTests'
     PACKAGE_NAME='0Ho1U000000CaUzSAK'
     
     SF_INSTANCE_URL = 'https://login.salesforce.com'
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
