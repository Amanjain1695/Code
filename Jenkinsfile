#!groovy

import groovy.json.JsonSlurperClassic

node {

    def SF_CONSUMER_KEY=env.CONNECTED_APP_CONSUMER_KEY_DH
    def SF_USERNAME=env.HUB_ORG_DH
    def SERVER_KEY_CREDENTALS_ID=env.JWT_CRED_ID_DH
    def TEST_LEVEL='RunLocalTests'
    def PACKAGE_NAME='0Ho1U000000CaUzSAK'
    def PACKAGE_VERSION
    def SF_INSTANCE_URL = env.SFDC_HOST_DH ?: "https://login.salesforce.com"

    def toolbelt = tool 'toolbelt'


    // -------------------------------------------------------------------------
    // Check out code from source control.
    // -------------------------------------------------------------------------

    stage('checkout source') {
        checkout scm
    }


    // -------------------------------------------------------------------------
    // Run all the enclosed stages with access to the Salesforce
    // JWT key credentials.
    // -------------------------------------------------------------------------
    
    withEnv(["HOME=${env.WORKSPACE}"]) {
        
        withCredentials([file(credentialsId: SERVER_KEY_CREDENTALS_ID, variable: 'server_key_file')]) {
            // -------------------------------------------------------------------------
            // Check versioof cli
            // -------------------------------------------------------------------------
              
            stage('Sfdxcli version') {
                rc = command "${toolbelt} sfdx version"
                if (rc != 0) {
                    error 'Salesforce installation failed.'
                }
            }
            // -------------------------------------------------------------------------
            // Authorize the Dev Hub org with JWT key and give it an alias.
            // -------------------------------------------------------------------------
            
            stage('Authorize DevHub') {
                rc = command "${toolbelt} sfdx force:auth:jwt:grant --instanceurl ${SF_INSTANCE_URL} --clientid ${SF_CONSUMER_KEY} --username ${SF_USERNAME} --jwtkeyfile ${'MIIEpAIBAAKCAQEAzVGtrWrpi/On5uYJTGIKd8CbNYAfYVNxWTX+o5nOnRkkcvzWyoz+14FhREXg6P1Q/H9lwNQpP/SshjOrjY6nZa7crc0OXqAb6fum4ZVZWafyi2/zgXqDDYdI36WLK2iA+5pNypczybRMhBYFP/xxi1MjFOk3T2hAXyNdsH08zEX6my6mhLXHNUKJQzmUmX0Znr6ugOYwCCVNHnaVWruqQYTJJNfvRHTQAENEyxBZQug7APmRr/ayMnBba0GUDIicZfQjbiQIbVWlqQqWzr54bFiTkswWyZZzquEj0XAmJT+pgvUHiEeNjAXSF/fVDWcf2Jztu4aX2CSn1iddsgPSfwIDAQABAoIBAF6Q1SZ/jIv6MIYnw3ab3WhknNgaZ9mi3h0RwnPFvqUa1G/lxmRKZoIJxCv2521IZ0m0v7/9t/YOEnxJRiWP48fwrxGZ1Zl9sv2k+6sA58NkmFDiwkwLilrryYPAsoXOv0GjQ1shIygu0+MuZUKgWgeqxgi2ldQMF0H6fwdv11XZvihuQdRp3GW9tGc6mSAbHXRd6YWzAF1zfkFCCrj7rqxg+pmHE/vIKUcApijP3AZxrlpyFSgV8ebl3GFqKwsYXfbRS7pXZMzmkKbvlnBzqYjvMKSehwsbloJWdUzosauI5m7Gbjd5PJKVT2iIAkxTZnYmBWLojqMiTk9p/LhbjrECgYEA6PPOtWCActmfL+1K2PLNl6o8ACFvcLwz6NoyxfXkfwue6K1npuXWCRQ3tFDWAx6XexS7umPfr/5sPKUZDkIeNbk56WGn+9aRXvDqRPo3+yUxA7D/EaZpPKPa7lq9AiLQa+u5qzGvsgNW2FV6Di5ir45pis8UyeFQvOLSPgS6Z8cCgYEA4aH6MVqov+AaPCCnmX31Ji2CJdThG3tNXvfW+075FDFHW6Y22ES8IR/70E9usyRtnMSSc3/doEP6urZlWD7MIKUvg8tf6Gxd7lEyycTESEQ0mdlPVYG8G022xSNDbptTZcspk3c9x7TwQz/NtBu3+bY8jMUGcm5Vo9BhMOylb4kCgYAs5pF5NFiNypR8UGiU2Hf4O7/E5qzsNdprj2Mp9PNN6Zd/kazg5nwS0+rIvqwBfewEtUJZ8tYyvf9u0QO7U9Mu17zp1wDh8cGjYxxEn1Ya+lgwNfV0GXc/UPXp62Ny/fLeWlk3PiR3U11x5UfZY+dxnymIr9F5+Avv3GhZu9+SEQKBgQCkoDNVGUmwnclmf4jplB5vGZsxES6hh4h/NyOTPx67He1rsE2p5BTDsntflOU3LegQDtiwDuZcjdz9qCEvjroPQ5b0eUnj4lVykaoVz0xLUgBzFDwvLjZaUYx+L+l+ZTQnPGF8Z+8arCj1WDM1K1hDiTSKnSLEET7JBDw1nyRhyQKBgQDOp/yc6jDgJHjGjQMhia+7F3K3NghJT1vHc3ae2o77mC55UJ6hsX1Q4Wq6w8lSPcifIsro/Ww/IGySnmlqeRpOaRfEZTCzzTxGuJ9Dg5qOeRuoQIuu+YC3Zgv6WGWwIPtLL2BXp9Uq28oD/w/e8h/UBC/5tY5CdCGyqYAMwWwhVQ=='} --setdefaultdevhubusername --setalias HubOrg"
                if (rc != 0) {
                    error 'Salesforce dev hub org authorization failed.'
                }
            }


            // -------------------------------------------------------------------------
            // Create new scratch org to test your code.
            // -------------------------------------------------------------------------

            stage('Create Test Scratch Org') {
                rc = command "${toolbelt} sfdx force:org:create --targetdevhubusername HubOrg --setdefaultusername --definitionfile config/project-scratch-def.json --wait 10 --durationdays 1"
                if (rc != 0) {
                    error 'Salesforce test scratch org creation failed.'
                }
            }


            // -------------------------------------------------------------------------
            // Display test scratch org info.
            // -------------------------------------------------------------------------

            stage('Display Test Scratch Org') {
                rc = command "${toolbelt} sfdx force:org:display"
                if (rc != 0) {
                    error 'Salesforce test scratch org display failed.'
                }
            }


            // -------------------------------------------------------------------------
            // Push source to test scratch org.
            // -------------------------------------------------------------------------

            stage('Push To Test Scratch Org') {
                rc = command "${toolbelt} sfdx force:source:push"
                if (rc != 0) {
                    error 'Salesforce push to test scratch org failed.'
                }
            }


            // -------------------------------------------------------------------------
            // Run unit tests in test scratch org.
            // -------------------------------------------------------------------------

            stage('Run Tests In Test Scratch Org') {
                rc = command "${toolbelt} sfdx force:apex:test:run --wait 10 --resultformat tap --codecoverage --testlevel ${TEST_LEVEL}"
                if (rc != 0) {
                    error 'Salesforce unit test run in test scratch org failed.'
                }
            }
        }
    }
}

def command(script) {
    if (isUnix()) {
        return sh(returnStatus: true, script: script);
    } else {
        return bat(returnStatus: true, script: script);
    }
}
