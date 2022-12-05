pipeline {
    agent any
    
    tools {
        maven 'Apache Maven 3.8.5'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '13.232.37.20', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
                        bat "scp -v -o StrictHostKeyChecking=no **/*.war root@${params.staging_server}:/opt/tomcat/webapps/"
                    }
                }
            }
        }
    }
}
