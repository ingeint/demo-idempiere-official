pipeline {
    agent {
        docker { image 'docker:19' }
    }
    environment {
        PROJECT_NAME = 'idempiere-demo-official'
        NETWORK_NAME = 'idempiere_demo_official'
        
    }
    stages {
        stage('Deploy iDempiere Demo') {
            steps {
                sh 'whoami'
                sh 'docker network create --driver overlay --scope swarm $NETWORK_NAME || true'
                sh 'docker stack rm $PROJECT_NAME || true'
                sh 'sleep 2'
                sh 'docker stack deploy -c docker-stack.yml $PROJECT_NAME'
                sh 'sleep 2'
                sh 'docker stack ps $PROJECT_NAME'
            }
        }
    }
}
