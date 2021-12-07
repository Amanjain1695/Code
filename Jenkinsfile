pipeline {
         agent any
         
                 
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
                
               //  stage('Four') {
               //  parallel { 
               //             stage('Unit Test') {
                 //          steps {
                 //               echo "Running the unit test..."
                   ///        }
                      //     }
                        //    stage('Integration test') {
                    //          
                    //       }
                      //     }
                        //   }
            
}
