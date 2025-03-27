pipeline {
    agent any
    stages {
        stage('Copy Files to EC2') {
            steps {
                sshagent(['ec2-deploy-key']) {  // Uses Jenkins SSH key
                    sh 'scp -r * ubuntu@<EC2_IP>:/home/ubuntu/app/'
                    sh 'ssh ubuntu@<EC2_IP> "ls -la /home/ubuntu/app/"'  // Verify
                }
            }
        }
    }
    post {
        success {
            echo "Files deployed to EC2! - t1"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}


