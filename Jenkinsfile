pipeline {
    agent any
    stages {
        stage('Test') {
        agent {
           docker {
             image 'maven:3-alpine'
             args '-v /root/.m2:/root/.m2'
           }
        }
                steps {
                 echo 'INFO: Testing....'
                 sh 'mvn test'
                }
        }
        stage('Build') {
        agent any
            steps {
                echo "INFO: Building Docker Image"
                sh 'mvn install'
                sh "docker build -t pipeline-demo:latest ."
                echo "INFO: Docker Image build"
            }
        }

        stage('Deploy') {
        agent any
            steps {
               echo "INFO : Running new Docker Image"
               sh "docker rm -f pipeline-demo:latest || true "
               sh "docker run --restart always  pipeline-demo:latest"
               echo "INFO : Deployed "
            }
        }
    }
}