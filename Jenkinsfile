pipeline {
    agent any
	tools {
              jdk "JAVA_HOME"
	      maven "MAVEN_HOME"
        }

    stages {
        stage('Checkout') {
            steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'devopsdeepdive', url: 'https://github.com/devopsdeepdive/maven-pipeline.git']]])            }
        }
    
     stage('Validate') {
            steps {
                sh 'mvn validate'
        }
    }
    
     stage('compile_code') {
            steps {
                sh 'mvn compile'
        }
    }
      stage('Test') {
            steps {
                sh 'mvn test'
        }
    }
     stage('Package') {
            steps {
                sh 'mvn package'
        }
    }
	     stage('deploy') {
            steps {
             sshagent(['tomcat-deploy']) {
   sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/maven-pipeline/target/maven-web-application.war ubuntu@172.31.43.182:/opt/apache-tomcat-9.0.62/webapps/"
}
        }
    }
	}
}
