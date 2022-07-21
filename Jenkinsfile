pipeline {
    agent {
        kubernetes {
            inheritFrom 'jenkins-slave'
            inheritFrom 'maven-docker-kubectl'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh "mvn clean package spring-boot:repackage"
                sh "printenv" // 将环境变量打印到 console 中
            }
        }
    }
}
