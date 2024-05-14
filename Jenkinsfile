pipeline {
    agent {
        label 'agent_node'
    }
    environment{
        DOCKER_HUB_PAT = credentials('PAT_Dockerhup')
    }
    stages {
        stage('Clone') {
            steps {
                 git branch: 'main', url: 'https://github.com/fredericEducentre/reactJS.git'
            }
        }
        stage('Build') {
            steps {
                sh '''
                    npm install
                    npm run build
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }
        stage('Delivery'){
            steps{
                sh 'docker login -u aekobo -p ${DOCKER_HUB_PAT}'
                sh 'docker build . -t aekobo/calcul_chauffage:${BUILD_ID}'
                sh 'docker push aekobo/calcul_chauffage:${BUILD_ID}'
            }
        }
    }
}

