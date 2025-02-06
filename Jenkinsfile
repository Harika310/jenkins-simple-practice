pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Harika310/roboshop-infra-dev.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploy') {
            steps {
                sh 'scp target/your-project.jar user@server:/path/to/deploy'
            }
        }
    }


    post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
        success{
            echo "This section run when pipeline success"
        }
        failure{
            echo "This section run when pipeline failure"
        }
    }
}