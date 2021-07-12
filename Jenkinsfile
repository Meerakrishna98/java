  
pipeline {
    agent {label 'agent' }
    tools { maven 'maven'}

    environment {
        CI = 'true'
        registry = 'docker-services-training/aleesha/'
        }
    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Sonarqube analysis') {
            steps {
                script {
                    withSonarQubeEnv('sonar'){
                        sh 'mvn sonar:sonar -DskipTests'
                     }
                 }
            }
        }
        
    }
}
