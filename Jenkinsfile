pipeline {
    agent any

    environment {
        USER = 'ubuntu'
        KEY_FILE = '/home/ubuntu/ansible_demokey.pem'
        WORKSPACE = '/opt/jenkins/workspace/ansible-pipeline'
    }

    stages {
        stage('Install Apache & Update Website') {
            steps {
                script {
                    // Run apache-install playbook
                    sh '''
                    export ANSIBLE_HOST_KEY_CHECKING=False
                    ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/inventory.ini $WORKSPACE/apache-install.yml
                    '''

                    // Run website-update playbook
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
                    // Run website-test playbook
                    sh '''
                    export ANSIBLE_ROLES_PATH=$WORKSPACE/roles
                    ansible-playbook -u $USER --private-key $KEY_FILE -i $WORKSPACE/inventory.ini $WORKSPACE/website-test.yml
                    '''
                }
            }
        }
    }
}
