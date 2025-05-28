pipeline {
    agent any

    tools {
        jdk 'JDK11'
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Linux ajan kullanıyorsan:
                sh 'mvn clean package -B'
                // Eğer Windows ajan kullanacaksan, aşağıdakinin yorumunu kaldır:
                // bat 'mvn clean package -B'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test -B'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build başarılı!'
        }
        failure {
            echo '❌ Build başarısız!'
        }
    }
}
