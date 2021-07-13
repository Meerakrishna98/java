pipeline {
    agent {label 'agent' }
    tools { maven 'maven'}

    environment {
        CI = 'true'
        registry = 'docker-awskeypair.pem/Meerakrishna/'
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
                    junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
                }
            }
        }
       // stage('Sonarqube analysis') {
         //   steps {
           //     script {
             //       withSonarQubeEnv('sonar'){
               //         sh 'mvn sonar:sonar -DskipTests'
                 //    }
                 //}
            //}
        //}
        // stage('Artifactory') {
        //     steps {
        //         script {
        //             docker.withTool('docker') {
        //                 docker.withRegistry('https://artifactory.dagility.com', 'aleesha-registry'){
        //                     docker.build(registry + "maven:latest").push()
        //                 }
        //             }
        //         }
        //     }
        // }
        stage('Email Notification'){ 
            steps {
                mail bcc: '', body: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', cc: 'nandaardra@gmail.com, mkmanakkalath31@gmail.com', from: '', replyTo: '', subject: 'Email Notification from Jenkins', to: 'meerakrishna19mr@gmail.com'
        }

    }
}
}
