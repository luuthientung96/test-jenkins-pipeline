pipeline {
    agent any
    stages {
        stage('Test') {
                steps {
                 echo 'INFO: Testing....'
                 sh "mvn test"
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
               sh "docker run --restart always -p 8082:8082 --name pipeline-demo:latest"
               echo "INFO : Deployed "
            }
        }
    }
}