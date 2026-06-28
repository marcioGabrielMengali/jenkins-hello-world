pipeline {
    agent any

    tools {
        maven "M398"
        jdk "JDK21"
    }

    stages{
        stage('Echo Version') {
            steps {
                sh 'echo Print Maven Version'
                sh 'mvn -version'
                sh 'echo Java Version'
                sh 'java -version'
            }
        }
        stage('Build'){
            steps {
                git branch: 'main', url: 'https://github.com/marcioGabrielMengali/jenkins-hello-world.git'
                sh "mvn clean package -DskipTests=true"
            }
        }
        stage('Unit Test'){
            steps {
                sh "mvn test"
            }
        }
    }
}