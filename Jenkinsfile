pipeline {
    agent {
        docker { image 'docker:19' }
    }
    environment {
        PROJECT_NAME = 'idempiere-demo-official'
        NETWORK_NAME = 'idempiere_demo_official'
        REGISTRY_PASS = credentials('ingeint-registry-pass')
    }
    stages {
        stage('Deploy iDempiere Demo') {
            steps {
                sh 'docker login $REGISTRY_REPOSITORY -u $REGISTRY_USER -p $REGISTRY_PASS'
                sh 'docker network create --driver overlay --scope swarm $NETWORK_NAME || true'
                sh 'docker stack rm $PROJECT_NAME || true'
                sh 'sleep 2'
                sh 'docker stack deploy --with-registry-auth -c docker-stack.yml $PROJECT_NAME'
                sh 'sleep 2'
                sh 'docker stack ps $PROJECT_NAME'
            }
        }
    }
}
