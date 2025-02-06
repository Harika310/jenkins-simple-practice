pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
                //sh 'sleep 10'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                
            }
        }
        stage('Deploy') {
            
            steps {

                    sh 'mvn deploy'
                    //error 'pipeline failed'

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