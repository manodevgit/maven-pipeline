pipeline {
    agent any
	tools {
              jdk "JAVA_HOME"
	      maven "MAVEN_HOME"
        }

    stages {
        stage('Checkout') {
            steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/devopsdeepdive/maven-pipeline.git']]])            }
        }
    
     stage('Validate') {
            steps {
                sh 'mvn validate'
        }
    }
    
     stage('Compile') {
            steps {
                sh 'mvn compile'
        }
    }
      stage('Test') {
            steps {
                sh 'mvn test'
        }
    }
     stage('Package_new') {
            steps {
                sh 'mvn package'
        }
    }
	    stage('Deploy') {
            steps {
             sshagent(['tomcat-deploy']) {
    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/maven-pipeline/target/maven-web-application.war ubuntu@13.233.133.251:/opt/apache-tomcat-9.0.63/webapps/"
}
        }
    }
	}
}
