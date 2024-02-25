pipeline {

    agent {
        node {
            label 'workstation'
        }
    }

    options {
        ansiColor('xterm')
    }

    parameters {
        choice(name: 'env', choices: ['dev', 'prod'], description: 'Pick Environment')

        string(name: 'component', defaultValue: '', description: 'Provide the Component Name')
    }

    stages {

        stage('Ansible') {
            steps {
                sh 'ansible-playbook -i ${component}-${env}.surendrababuc01.online, roboshop.yml -e ansible_user=centos -e ansible_password=DevOps321 -e env=${env} -e role_name=${component}'
            }
        }

        stage('Ansible') {
            steps {
                sh ' aws ec2 describe-instances --filters "Name=tag:Name,Values={component}-${env}" --query \'Reservations[*].Instances[*].PrivateIpAddress\' --output text\n >>/tmp/inv'
                sh 'ansible-playbook -i /tmp/inv, roboshop.yml -e ansible_user=centos -e ansible_password=DevOps321 -e env=${env} -e role_name=${component}'
            }
        }

    }

    post {
        always {
            cleanWs()
        }
    }
}