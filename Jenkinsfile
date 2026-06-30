pipeline {
    agent any

    tools {
        maven 'M398'
        jdk 'JDK17'
    }

    stages {
        stage('Maven Version') {
            steps {
                sh 'echo Print Maven Version'
                sh 'mvn -version'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
                archiveArtifacts artifacts: 'target/hello-demo-*.jar', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                junit testResults: 'target/surefire-reports/TEST-*.xml', keepProperties: true, keepTestNames: true
            }
        }
        stage('Local Deployment'){
            steps {
                sh 'java -jar target/hello-demo-*.jar > /dev/null &'
            }
        }
        stage('Integration Test'){
            steps {
                sh 'sleep 5s'
                sh 'curl -X GET http://localhost:6767/hello'
            }
        }
    }
}
