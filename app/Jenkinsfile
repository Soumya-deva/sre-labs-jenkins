/* groovylint-disable LineLength */
pipeline {
    agent any
    stages {
        stage('Docker Build') {
            steps {
                sh 'docker build -f containerfile -t chetanguptahcl/frontend:jen .'
            }
        }
        stage('Docker Push') {
            agent any
            steps {
                withCredentials([usernamePassword(credentialsId: 'd5a41b0b-390b-428e-bf78-0d710dbc225e', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login docker.io -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh 'docker push chetanguptahcl/frontend:jen'
                }
            }
        }
        stage('Docker Run') {
            agent any
            steps {
                sh 'docker run -d -p 12000:12000 chetanguptahcl/frontend:jen'
                }
            }
        }
    }
