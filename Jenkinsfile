pipeline {
         agent any
         stages {
         
                 
                 stage('One') {
                 agent {
                                    docker {
                                            reuseNode true
                                            image 'salesforce/salesforcedx:latest-full'
                                           }
                                    }
                              steps {
                                echo "Running the integration test..."
                                sh 'sfdx version'
                              }
                 }
         }
}
