pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'devopsdeepdive', url: 'https://github.com/devopsdeepdive/maven-pipeline.git']]])            }
        }
    }
     stage('validate') {
            steps {
                sh 'mvn validate'
        }
    }
    
     stage('compile') {
            steps {
                sh 'mvn compile'
        }
    }
      stage('test') {
            steps {
                sh 'mvn test'
        }
    }
     stage('test') {
            steps {
                sh 'mvn package'
        }
    }
}
