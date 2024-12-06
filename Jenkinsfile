pipeline{
    agent any
    environment{
        MONGO_URL = 'mongodb://127.0.0.1/testDb'
    }
    tools{nodejs "nodeJS_latest"}
    stages{
        stage('check node version'){
            steps{
                bat 'node -v'
                bat 'npm -v'
            }
        }
        stage('Checkout'){
            steps{
                checkout([$class: 'GitSCM',
                branches: [[name '*/main']],
                userRemoteConfigs: [[url: 'https://github.com/FatimaMalik9/Integrate-and-deploy-mean-app.git']]
                ])
            }
        }
        stage('Install Dependencies'){
                steps{
                    dir('Mocha/restapi-testing'){
                        bat 'npm install'
                    }
                }
            }
        stage('Test'){
                steps{
                    dir('Mocha/restapi-testing'){
                        bat 'npm test'
                    
                }
            }
        }
    }
}