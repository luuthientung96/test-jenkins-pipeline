pipeline {
    agent any
    tools {
            maven 'Maven 3.5.2'
            jdk 'jdk8'
        }
    stages {
        stage('Test') {
                steps {
                 echo 'INFO: Testing....'
                 sh 'mvn -Dmaven.test.failure.ignore=true install'
                }
        }
        stage('Build') {
            steps {
                echo "INFO: Building Docker Image"
                sh "docker build -t pipeline-demo:latest ."
                echo "INFO: Docker Image build"
            }
        }

        stage('Deploy') {
            steps {
               echo "INFO : Running new Docker Image"
               sh "docker rm -f pipeline-demo:latest || true "
               sh "docker run --restart always -p 8082:8082 --name pipeline-demo pipeline-demo:latest"
               echo "INFO : Deployed "
            }
        }
    }
}