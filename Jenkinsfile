pipeline {
    agent any

    environment {
        registry = "mooneshbmsit/my-app"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }

    stages {
        stage ('checkout') {
            steps {
                git credentialsId: 'mooneshbmsit-git', url: 'https://github.com/mooneshbmsit/shared-hello-world.git', branch: 'main'
            }
        }
        stage ('Build image') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        stage ('Push image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        } 
        stage ('checkout') {
            steps {
                git credentialsId: 'mooneshbmsit-git', url: 'https://github.com/mooneshbmsit/dummy_nginx_helm.git', branch: 'main'
            }
        }
        stage ('Pull nxinx image') {
            stpes {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.pull
                    }
                }
            }
        }
        stage ('Deploy chart') {
            stpes {
                script {
                    sh "helm upgrade nginx-server"
                }
            }
        }
    }
}
