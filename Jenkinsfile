pipeline {
     agent any
     tools {
         maven 'MAVEN'
     }
     stages {
         stage('Build') {
             steps {
                 echo 'Hello World'
                 checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Meerakrishna98/java.git']]])
                 sh "mvn -Dmaven.test.failure.ignore=true clean package"
             }
         }
     }
}
