pipeline {
    agent { label 'agentfarm' }

    environment {
        USER = 'ubuntu'
        KEY_FILE = '/home/ubuntu/ansible_demokey.pem'
        WORKSPACE = '/opt/jenkins/workspace/ansible-pipeline'
    }

    stages {

        stage('Send Slack Notification') {
            steps {
                slackSend color: 'warning', message: "Please approve the deployment for *${env.JOB_NAME}* #${env.BUILD_NUMBER}. (<${env.BUILD_URL}|Open>)"
            }
        }

        stage('Request Approval') {
            steps {
                input message: 'Do you want to proceed with the deployment?'
            }
        }

        stage('Install Apache & Update Website') {
            steps {
                script {
                    sh '''
                    export ANSIBLE_HOST_KEY_CHECKING=False
                    ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/inventory.ini $WORKSPACE/apache-install.yml
                    '''

                    sh '''
                    export ANSIBLE_ROLES_PATH=$WORKSPACE/roles
                    ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/inventory.ini $WORKSPACE/website-update.yml
                    '''
                }
            }
        }

        stage('Test Website') {
            steps {
                script {
                    sh '''
                    export ANSIBLE_ROLES_PATH=$WORKSPACE/roles
                    ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/inventory.ini $WORKSPACE/website-test.yml
                    '''
                }
            }
        }
    }

    post {
        success {
            slackSend color: 'good', message: "✅ Build *${env.JOB_NAME}* #${env.BUILD_NUMBER} was successful!"
        }
        failure {
            slackSend color: 'danger', message: "❌ Build *${env.JOB_NAME}* #${env.BUILD_NUMBER} failed!"
        }
    }
}
