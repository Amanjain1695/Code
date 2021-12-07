pipeline {
         
         agent {
                                    docker {
                                            reuseNode true
                                            image 'salesforce/salesforcedx:latest-full'
                                           }
                                    }

     stages {
       
           // -------------------------------------------------------------------------
            // Check Version
            // -------------------------------------------------------------------------
       stage('Version Check') {
                              steps {
                                echo "Running the Version Check"
                                sh 'sfdx version'
                              }
                 }
       
            // -------------------------------------------------------------------------
            // Authorize the Dev Hub org with JWT key and give it an alias.
            // -------------------------------------------------------------------------
       
       stage('Authorize DevHub') {
                              steps {
                                echo "Authorize DevHub"
                                sh 'sfdx force:auth:jwt:grant --instanceurl https://login.salesforce.com --clientid 3MVG9pRzvMkjMb6nKN_QGvi32g_ZANpKZaYFpiOoonEynTpKJXumZp439yEPg0zccOkWGAVleKqNImUq5ZCqu --username ratneshkumar1166@gmail.com --jwtkeyfile ${server_key_file} --setdefaultdevhubusername --setalias HubOrg'
                              }
                 }
       
            // -------------------------------------------------------------------------
            // Create new scratch org to test your code.
            // -------------------------------------------------------------------------
       
       stage('Create Test Scratch Org') {
                              steps {
                                echo "Create Test Scratch Org"
                                sh 'sfdx force:org:create --targetdevhubusername HubOrg --setdefaultusername --definitionfile config/project-scratch-def.json --wait 10 --durationdays 1'
                              }
                 }
       
            // -------------------------------------------------------------------------
            // Display test scratch org info.
            // -------------------------------------------------------------------------
       
       stage('Display Test Scratch Org') {
                              steps {
                                echo "Display Test Scratch Org"
                                sh 'sfdx force:org:display'
                              }
                 }
       
            // -------------------------------------------------------------------------
            // Push source to test scratch org.
            // -------------------------------------------------------------------------
       
       stage('Push To Test Scratch Org') {
                              steps {
                                echo "Push To Test Scratch Org"
                                sh 'sfdx force:source:push'
                              }
                 }
       
            // -------------------------------------------------------------------------
            // Run unit tests in test scratch org.
            // -------------------------------------------------------------------------
       
       stage('Run Tests In Test Scratch Org') {
                              steps {
                                echo "Run Tests In Test Scratch Org"
                                sh 'sfdx force:apex:test:run --wait 10 --resultformat tap --codecoverage --testlevel ${TEST_LEVEL}'
                              }
                 }
         }
}
