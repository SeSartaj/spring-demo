pipeline {
    agent any

    triggers {
        githubPush()
    }

    tools {
        maven 'Maven 3.8.1' // configure Maven in Jenkins Global Tool Configuration
        jdk 'Java 17'       // configure Java in Jenkins Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sesartaj/spring-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'pkill -f "spring-boot-hello" || true'
                sh 'nohup java -jar target/*.jar --server.port=8081 > app.log 2>&1 & echo $! > app.pid'
            }
        }
    }
}
