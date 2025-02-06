pipeline {
    agent {
        label 'agent-1'
    }
    options {
       timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    environment {
        DEBUG = 'true'
        appVersion = '' // this will become global, we can use across pipeline
        region = 'us-east-1'
        account_id = '905418172435'
        project = 'expense'
        environment = 'dev'
        component = 'backend'
    }
    // install pipeline utilitysteps plugin in jenkins
    stages {
        stage('Read the version') {
             steps {
                // groovy script
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App version: ${appVersion}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
               
                sh 'npm install'
                
            }
        }
        stage('Docker Build') {
            steps {
                withAWS(region: 'us-east-1', credentials: 'aws-creds') {
                    sh """
                    docker build -t harika402/backend:${appVersion} .

                    docker images
                    """
                }
            }
           
        }


    }
    post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
        success {
            mail to: 'harikaeravathri@gmail.com',
                subject: "Successful Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build was successful!"
            echo "Email notification sent for successful build"
        }
        failure {
            mail to: 'harikaeravathri@gmail.com',
                subject: "Failed Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build failed!"
            echo "Email notification sent for failed build"
        }
    }
}