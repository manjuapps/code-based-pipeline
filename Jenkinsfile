pipeline {
    agent any

	tools {
        maven 'localMaven'
    }

    parameters {
         string(name: 'tomcat_dev', defaultValue: '3.17.36.162', description: 'Dev Server')
         string(name: 'tomcat_prod', defaultValue: '127.0.0.1', description: 'Production Server')
    }

stages{
        stage('Build'){
            steps {
				echo 'starting build step'
                bat 'mvn clean package'
				echo 'mvn command executed'
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
                stage ("Deploy to Production"){
                    steps {
                         bat "pscp -i /c/Users/msajja/Desktop/Udemy/Jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }
								
               
            }
        }
    }
}