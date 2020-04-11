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
                bat 'copy /Y "**/target/*.war" "C:\"'
            }
        }
    }
}
