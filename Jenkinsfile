pipeline {
    agent any
 
    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }
 
stages{
        stage('Build'){
            steps {
               build job: 'Hello_Jenkins ' 
            }
            post {
                success {
                    echo 'Tested Jenkins Code File...'
                }
            }
        }
 
        stage ('Deployments'){
            parallel{
                stage ('Ansible Hostname Playbook'){
                    steps {
                       build job: 'Run Ansible Playbook '
                    }
                post { 
                    success {
                      echo "Ready for Ansible Production"
                    }
                  }
                }
 
                stage ('Ansible Common Playbook'){
                    steps {
                       sh '/usr/local/bin/ansible-playbook /etc/ansible/test/common.yml -i /etc/ansible/hosts'
                    }
                }
            }
        }
    }
}
