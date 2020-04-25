 environment {
        GROOVY_HOME = tool name: 'Groovy-2.4.9', type: 'hudson.plugins.groovy.GroovyInstallation'
    }
    stages {
        stage('Run Groovy') {
            steps {
                bat "${groovy_home}/bin/groovy <script.name>"
            }
        }
    }

pipeline {
  agent any 
  tools {
   Maven 'maven'
  }
  
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
       
   
    
  
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    
    stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@13.234.66.200:/prod/apache-tomcat-8.5.54/webapps/webapp.war'
              }      
           }       
    }
    
    
    
    
  }
}
