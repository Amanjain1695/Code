pipeline {
    agent {
        docker {
            image 'curlybracket/salesforce:latest'
           
        }
    }
     echo "inside docker"
    stage('Add other packages') {
    echo "Installing A"
    timeout(900) {
        waitUntil {
            sh "sfdx force:package:install --package --wait 15"
        }
    }
    echo "A installed"
    }
    stages {
        stage('Test') {
            steps {
                
                sh 'node --version'
            }
        }
    }echo"Inside Stage"
}
