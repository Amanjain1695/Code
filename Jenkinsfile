#!groovy

import groovy.json.JsonSlurperClassic

pipeline {
         
         agent {
                                    docker {
                                            reuseNode true
                                            image 'salesforce/salesforcedx:latest-full'
                                           }
                                    }
    def SF_CONSUMER_KEY=env.CONNECTED_APP_CONSUMER_KEY_DH
    def SF_USERNAME=env.HUB_ORG_DH
    def SERVER_KEY_CREDENTALS_ID=env.JWT_CRED_ID_DH
    def TEST_LEVEL='RunLocalTests'
    def PACKAGE_NAME='0Ho1U000000CaUzSAK'
    def PACKAGE_VERSION
    def SF_INSTANCE_URL = env.SFDC_HOST_DH ?: "https://login.salesforce.com"
    
     stages {     
    // -------------------------------------------------------------------------
    // Check out code from source control.
    // -------------------------------------------------------------------------

    stage('checkout source') {
        checkout scm
    }

        
                 stage('One') {
                              steps {
                                echo "Running the integration test..."
                                sh 'sfdx version'
                              }
                 }
         }
}
