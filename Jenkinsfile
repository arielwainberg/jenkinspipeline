pipeline {
    agent any
    
    parameters { 
         string(name: 'tomcat_dev', defaultValue: '10.12.100.145', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '10.12.100.146', description: 'Production Server')
    } 

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i //var/lib/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat8/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        scp your_username@remotehost.edu:foobar.txt /some/local/directory
                        sh "scp -i /var/lib/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps"
                    }
                }
            }
        }
    }
}