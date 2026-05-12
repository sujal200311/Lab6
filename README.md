Pipeline Script:

    pipeline {
    agent any
   
    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sujal200311/Lab6'

            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
    }
    post {
        always {
                    junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'

        }
    }
}
