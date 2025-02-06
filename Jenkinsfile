pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Harika310/jenkins-simple-practice.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean install'
                //sh 'sleep 10'
                }
                
            }
        }
        stage('Test') {
            steps {
                script {
                     sh 'mvn test'
                }
               
                
            }
        }
        stage('Deploy') {
            
            steps {
                script {
                    sh 'mvn deploy'
                    //error 'pipeline failed'
                }
                    

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