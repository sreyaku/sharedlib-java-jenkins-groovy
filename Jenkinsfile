@Library('jenkins-shared-library-groovy-practice') _
pipeline {
    agent any
stages{
        stage('SonarQube Scan'){
            steps {
                script{
                    scan()
                }
               
            }
        }
            stage('Java_build') {
                steps {
                    script{
                        java_build()
                
                }
                     post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
            }
        }
                stage ("Deploy to Staging"){
                    steps {
                        script{
                            deploy()
                       
                }
            }
        }
//     stage ("Upload to S3"){
//         steps {
//             script{
//                 upload()
//             }
//         }
    }
    }

