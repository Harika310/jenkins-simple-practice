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
                docker build -t harika402/backend: ${appVersion} .
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
        success{
            echo "mail to: harikaeravathri@gmail.com"
            echo "subject: Successful Build: ${project} #${environment}"
        }
        failure{
            echo "mail to: harikaeravathri@gmail.com"
            echo "subject: Successful Build: ${project} #${environment}"
        }
    }
}



// trigger same pipeline for different regions
/* pipeline {
    agent any

    parameters {
        choice(name: 'REGION', choices: ['us-east', 'us-west', 'eu-central'], description: 'Select the region to deploy')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/your-project.git'
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
                script {
                    if (params.REGION == 'us-east') {
                        sh 'scp target/your-project.jar user@us-east-server:/path/to/deploy'
                    } else if (params.REGION == 'us-west') {
                        sh 'scp target/your-project.jar user@us-west-server:/path/to/deploy'
                    } else if (params.REGION == 'eu-central') {
                        sh 'scp target/your-project.jar user@eu-central-server:/path/to/deploy'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            deleteDir() // Clean up workspace
        }
        success {
            mail to: 'team@example.com',
                 subject: "Successful Build: ${env.JOB_NAME} #${env.BUILD_NUMBER} in ${params.REGION}",
                 body: "Good job! The build ${env.JOB_NAME} #${env.BUILD_NUMBER} for region ${params.REGION} completed successfully."
        }
        failure {
            mail to: 'team@example.com',
                 subject: "Failed Build: ${env.JOB_NAME} #${env.BUILD_NUMBER} in ${params.REGION}",
                 body: "The build ${env.JOB_NAME} #${env.BUILD_NUMBER} for region ${params.REGION} failed. Please check the logs."
        }
    }
} */
