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
                    git credentialsId: '63aa33e1-2c90-468f-8946-d612935168b6', url: 'https://github.com/ystroog/devops.git'
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
                    sh "cd /&& cd /var/jenkins_home/ && ls"
                    sh "echo $HOST >> hosts"
                    sh "/usr/bin/ansible-playbook -i hosts  -u centos -b --private-key=/var/jenkins_home/ansible/my.pem /var/jenkins_home/workspace/jenkinsfile_ansible/dockerplaybook.yml"
                    sh 'rm hosts'
                }
            }

