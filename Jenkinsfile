pipeline {
    agent {
        kubernetes {
            inheritFrom 'jenkins-slave'
            inheritFrom 'maven-docker-kubectl'
        }
    }
    
    environment {
        // gitlab auth
        GITLAB_URL = "http://39.97.192.108:8088/bsh-wuxiaobao/manager-api.git"
        GITLAB_BRANCH = "master"
        GITLAB_CREDENTIAL = "wxb-prod-code-pull-user"
        
        //docker registry auth
        REGISTRY = "http://10.0.1.135:8080"
        REGISTRY_CREDENTIAL = "bsh-prod-harbor-auth"
        
        //k8s auth
        KUBERNETES_CREDENTIAL  = "bsh-prod-k8s-kubectl-auth"
    }
    
    stages {
        stage('Test Pull Source Code') {
            steps {
                git branch: "${GITLAB_BRANCH}", credentialsId: "${GITLAB_CREDENTIAL}", url: "${GITLAB_URL}"
            }
        }
        
        stage ('Test Maven') {
            steps {
                container('maven') {
                    sh 'mvn -version'
                }
            }
        }
        
        stage ('Test Docker') {
            steps {
                container('docker') {
                    script{
                        sh 'docker info'
                        docker.withRegistry( REGISTRY,REGISTRY_CREDENTIAL ){
                            
                        }
                    }
                }
            }
        }
        
        stage ('Test Kubectl') {
            steps {
                container('kubectl') {
                    script{
                        withKubeConfig([credentialsId: "${KUBERNETES_CREDENTIAL}"]) {
                            sh "kubectl get node -o wide"
                        }
                    }
                }
            }
        }
    }
}
