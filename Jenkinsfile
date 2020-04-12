pipeline {
    agent any

    parameters {
         string(name: 'tomcat_aws', defaultValue: '13.234.177.90', description: 'AWS Tomcat Server')
    }

    triggers {
         pollSCM('* * * * *')
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
        stage ('Deploy to Staging'){
            steps {
                        sh "scp -i /home/ec2-user/ec2keyvalue.pem **/target/*.war ec2-user@${params.tomcat_aws}:/var/lib/tomcat8/webapps"
            }
        }
    }
}
