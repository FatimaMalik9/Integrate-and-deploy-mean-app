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
                branches: [[name: '*/main']],
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
        stage('Archive Artifacts'){
            steps{
                dir('Mocha/restapi-testing'){
                    archiveArtifacts artifacts: 'test-results.xml, coverage/**', allowEmptyArchive:true

                    //archiveArtifacts artifacts : 'mochawesome-report/**/*',allowEmptyArchive: true
                }
            }
        }
    }
    post{
        always{
            junit 'test-results.xml'
            // emailext(
            //     to: 'fm460417@gmail.com',
            //     subject: "Build ${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
            //     body: """<p>Build ${env.BUILD_NUMBER} - ${currentBuild.currentResult}</p>
            //     <p><a href="${env.BUILD_URL}artifact/mochawesone-report/index.html">View Test Report</a></p>""",
            //     attachLog: true,
            //     attachmentsPattern: 'mochawesome-report/**/*'
            // )
       }
    }

}      
       


