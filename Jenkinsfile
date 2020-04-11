pipeline {
    agent any

    parameters {
         string(name: 'tomcatServer', defaultValue: 'localhost', description: 'Tomcat Server')
    }

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deploy'){
            steps {
                bat "copy **/target/*.war C:/Softwares/TomcatForJenkins/apache-tomcat-8.5.54/webapps"
            }
        }
    }
}