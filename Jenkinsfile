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
                sh "echo Sleep Time - ${params.SLEEP_TIME}, Port - ${params.APP_PORT}, Branch - ${params.BRANCH_NAME}"
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
                sh "sleep ${params.SLEEP_TIME}"
                sh "curl -X GET http://localhost:${params.APP_PORT}/hello"
            }
        }
    }
}
