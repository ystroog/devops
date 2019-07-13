def ls_command  
pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('checkout'){
            steps {
                script {
                    cleanWs()
                    git credentialsId: '04183fb4-b64b-48f3-915b-33508577ba9d', url: 'https://github.com/ystroog/devops.git'
                    sh 'ls'
                }
            }
        }
        stage('Ansible Playbook') {
             input{
                message 'Enter Host'
                    id 'Host'
                    ok 'OK'
                    parameters {
                        string defaultValue: 'Host', description: '', name: 'HOST', trim: false
                    }
             }
                
            steps {
                script {
                    sh "cd /&& cd /opt/jenkins_home/ && ls"
                    sh "echo $HOST >> hosts"
                    sh "ansible-playbook -i hosts  -u centos -b --private-key=/var/jenkins_home/ansible/my.pem /opt/jenkins_home/jenkinsfile_ansible/dockerplaybook.yml"
                    sh 'rm hosts'
                }
            }
        }
    }
}
