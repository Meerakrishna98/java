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
                    //S
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
        //stage('Sonarqube analysis') {
        //    steps {
        //        script {
        //            withSonarQubeEnv('sonar'){
          //              sh 'mvn sonar:sonar -DskipTests'
         //            }
          //       }
        //    }
      //  }
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
        stages {
        stage('Ok') {
            steps {
                echo "Ok"
            }
        }
    }
    post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }
}

    }
}
