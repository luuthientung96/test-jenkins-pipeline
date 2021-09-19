pipeline {
    agent any
    stages {
        stage('Test') {
        agent {
           label 'master'
        }
                steps {
                 echo 'INFO: Testing....'
                 sh 'mvn -Dmaven.test.failure.ignore=true install'
                }
        }
        stage('Build') {
        agent any
            steps {
                echo "INFO: Building Docker Image"
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