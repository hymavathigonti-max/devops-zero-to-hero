pipeline {
    agent any

    stages {

        stage('Verify SSH to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@13.232.123.232 "
                    hostname
                    whoami
                    pwd
                    "
                    '''
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@13.232.123.232 "
                    cd ~/devops-zero-to-hero &&

                    git pull origin main &&

                    docker stop devops-app || true &&
                    docker rm devops-app || true &&

                    docker build -t devops-app1:v2 . &&

                    docker run -d \
                    --name devops-app \
                    -p 80:80 \
                    devops-app1:v2
                    "
                    '''
                }
            }
        }
    }
}