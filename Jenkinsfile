pipeline {
    agent any
     }
 
stages{
        stage('Build'){
            steps {
               build job: 'Hello Jenkins ' 
            }
            post {
                success {
                    echo 'Tested Jenkins Code File...'
                }
            }
        }
         stage ('Ansible Hostname Playbook'){
             steps {
                build job: 'Run_Ansible_Playbook '
                    }
             post { 
             success {
              echo "Ready for Ansible Production"
                    }
                  
             failure { 
              echo "Not Ready for Production"
             }
             }
                }
         stage ('Ansible Common Playbook'){
            steps {
                  timeout (time:1, unit: 'DAYS'){
                      input message: 'Approve PRODUCTION Deployment?'
                  }
                  build job: 'Run_Ansible_Playbook_to_Production'
                    }
                }
            }
