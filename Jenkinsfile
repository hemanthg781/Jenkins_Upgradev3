pipeline {
      agent any
          triggers {
             cron('0 */5 * * *')
                
          #!/bin/bash
            echo "hello, today is $(date)" > /tmp/hemanth.txt    
          
          }
      
      stages {
            stage('DEV') {
                  steps {
                        echo 'Hi Hemanth, this is DEV Stage'
                        
                  }
            }
            stage('UAT') {
                  steps {
                        echo 'Hi Hemanth, this is UAT Stage'
                  }
            }
            stage('PROD') {
                  steps {
                        echo "Hi Hemanth, this is PROD Stage"
                  }
            }
            
            stage('Publish') {
                   when {
                         branch 'master'
                        }
                   steps {
                          withDockerRegistry([ credentialsId: "dockerlogin", url: "" ]) {
                          sh 'docker push hemanthg781/terraform:latest'
                          sh 'docker push hemanthg781/cli:latest'
        }
      }
    }
      }
      
      post {
        always {
            emailext body: 'A Test EMail - Build is success', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }
}
