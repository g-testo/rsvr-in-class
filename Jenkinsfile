pipeline {
    agent none
    stages {
        stage('Setup Environment') {
            steps {
                sh 'source /etc/profile'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Build Jar') { 
            steps {
                sh 'mvn package' 
            }
        }
        stage('Containerize') { 
            steps {
                sh 'docker build -t rsvrproject ../deliverables' 
            }
        }
    }
}