pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds() 
        retry(2)
        timeout(time: 20, unit: 'MINUTES')
    }
    parameters{
        string(
            name: 'BRACH', defaultValue: 'main', description: 'branch to build?'
        )
        choice(
            name: 'ENV', choices: ['qa', 'dev', 'prod'], description: 'environment to build'
        )
    }
    stages{
        stage('docker login and push'){
            steps{
                sh "docker login -u <user_name> -p <password>"
                sh '''
                      cd vote
                      docker build -t <user_name>/vote:v${BUILD_NUMBER} .
                   '''
                sh "docker push <user_name>/vote:v${BUILD_NUMBER}"

            }
        }
        stage("display"){
            steps{
                sh "echo starting deployment"
            }
        }
    }

}
