pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/subhakanth1805-sudo/devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-app .'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@54.235.51.242 << EOF
                    docker stop devops-app || true
                    docker rm devops-app || true
                    docker build -t devops-app /home/ubuntu/devops-project
                    docker run -d -p 3000:3000 devops-app
                    EOF
                    '''
                }
            }
        }
    }
}