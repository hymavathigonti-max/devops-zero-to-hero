pipeline {
    agent any

    stages {

        stage('Verify SSH to EC2') {
            steps {
                sshagent(credentials: ['ec2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@13.232.123.232 "hostname && whoami && pwd"
                    '''
                }
            }
        }
    }
}