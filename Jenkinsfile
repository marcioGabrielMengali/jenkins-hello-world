pipeline {
    agent any

    tools {
        maven 'M398'
        jdk 'JDK17'
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/marcioGabrielMengali/jenkins-hello-world.git'
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

        stage('Containerization') {
            steps {
                sh 'echo Docker Build Image....'
                sh 'echo Docker Tag Image....'
                sh 'echo Docker Push Image....'
            }
        }

        stage('Kubernetes Deployment') {
            steps {
                sh 'echo Deploy to Kubernetes usig ArgoCD'
            }
        }

        stage('Integration Test') {
            steps {
                sh 'sleep 10s'
                sh 'echo Testing using cURL commands....'
            }
        }
    }
}
