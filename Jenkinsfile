pipeline {
    agent {
        kubernetes {
            inheritFrom 'jenkins-slave'
            inheritFrom 'maven-docker-kubectl'
        }
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
