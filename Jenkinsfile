pipeline {
    agent any

    tools {
        maven 'M398'
        jdk 'JDK17'
    }

    stages {
        stage('Echo Version') {
            steps {
                sh 'echo Print Maven Version'
                sh 'mvn -version'
                sh 'echo Java Version'
                sh 'java -version'
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/marcioGabrielMengali/jenkins-hello-world.git'
                sh 'mvn clean package -DskipTests=true'
                archiveArtifacts artifacts: 'target/hello-demo-*.jar', fingerprint: true
            }
        }
        stage('Unit Test') {
            steps {
                sh 'mvn test'
                junit testResults: 'target/surefire-reports/TEST-*.xml', keepProperties: true, keepTestNames: true
            }
        }
    }
}
