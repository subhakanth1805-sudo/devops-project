stage('Deploy to EC2') {
    steps {
        sshagent(['ec2-key']) {
            sh '''
            ssh -o StrictHostKeyChecking=no ubuntu@54.235.51.242 "
            docker stop devops-app || true &&
            docker rm devops-app || true &&
            cd /home/ubuntu/devops-project &&
            git pull &&
            docker build -t devops-app . &&
            docker run -d -p 3000:3000 devops-app
            "
            '''
        }
    }
}