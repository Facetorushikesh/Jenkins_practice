pipeline {
    agent any
    
    environment{
        MAX_SIZE = 10
        MIN_SIZE = 1
    }
    
    parameters {
      choice choices: ["DEVELOPMENT","STAGING","PRODUCTION"], description: 'Please select the environment', name: 'ENVIRONMENT'
      password defaultValue: '123ABC', description: 'Please add the api key', name: 'APIKEY'
      text defaultValue: 'This is a change log', description: 'Please add the change log', name: 'CHANGELOG'
    }

    stages{
        stage('checkout'){
            environment{
                MAX_SIZE = 100
                MIN_SIZE = 50
            }
            steps{
                echo "this is test pipeline"
                echo "MAX SIZE: ${MAX_SIZE}"
                echo "MIN SIZE: ${MIN_SIZE}"
            }
        }
        
        stage('Build'){
            when{
                expression { params.ENVIRONMENT == "PRODUCTION" }
            }
            steps{
                echo "This is a ${ENVIRONMENT} environment"
            }
        }
        
        stage('Report'){
            steps{
                echo "This stage generate the report"
                sh "printf \"${params.CHANGELOG}\" > ${params.ENVIRONMENT}.txt"
                archiveArtifacts allowEmptyArchive: true, 
                    artifacts: '*.txt', 
                    fingerprint: true, 
                    followSymlinks: false, 
                    onlyIfSuccessful: true
            }
        }
    }
}
