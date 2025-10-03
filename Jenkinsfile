pipeline {
    agent any

    tools {
        maven 'Maven 3.8.1'  // configure Maven in Jenkins
        jdk 'Java 17'        // configure Java in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/<username>/spring-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh './mvnw test'
            }
        }
        stage('Run') {
            steps {
                sh 'pkill -f spring-demo || true'
                sh 'nohup java -jar target/*.jar --server.port=8081 > app.log 2>&1 & echo $! > app.pid'
            }
        }
    }
}
