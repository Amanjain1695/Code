pipeline {
         
         agent {
                                    docker {
                                            reuseNode true
                                            image 'salesforce/salesforcedx:latest-full'
                                           }
                                    }
         stages {
                 stage('One') {
                              steps {
                                echo "Running the integration test..."
                                sh 'sfdx version'
                              }
                 }
         }
}
