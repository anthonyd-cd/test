pipeline {
    agent any
 
    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }
 
stages{
        stage('Build'){
            steps {
                echo "from Jenkins Code File"
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
                        sh "#!/bin/bash"
                        "/usr/local/bin/ansible-playbook /etc/ansible/test/hostname.yml -i /etc/ansible/hosts"
                    }
                post { 
                    success {
                      echo "Ready for Ansible Production"
                    }
                  }
                }
 
                stage ('Ansible Common Playbook'){
                    steps {
                       sh "#!/bin/bash"
                       /usr/local/bin/ansible-playbook /etc/ansible/test/common.yml -i /etc/ansible/hosts  
                    }
                }
            }
        }
    }
}
