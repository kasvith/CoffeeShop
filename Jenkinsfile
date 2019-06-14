pipeline {
    agent any
    environment {
        CI = 'true'
        API = './CoffeeAPI'
    }
    stages {
        stage('Setup APIM Environments'){
            steps{
                sh './config.sh'
            }
        }
        stage('Deploy to Test') {
            environment{
                ENV = 'test'
            }
            steps {
                echo 'Deploying to Test'
                withCredentials([usernamePassword(credentialsId: 'apim', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'apimcli import-api -f $API -e $ENV -u $USERNAME -p $PASSWORD -k --preserve-provider=false --update --verbose'
                }
            }
        }
        stage('Deploy to Production') {
            environment{
                ENV = 'prod'
            }
            steps {
                echo 'Deploying to Production'
                withCredentials([usernamePassword(credentialsId: 'apim', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'apimcli import-api -f $API -e $ENV -u $USERNAME -p $PASSWORD -k --preserve-provider=false --update --verbose'
                }
            }
        }
    }
}
