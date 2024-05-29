pipeline {
    agent none
    tools {
        jdk 'JDK 17'  // Ensure 'JDK 17' is correctly configured in Jenkins Global Tool Configuration
        maven 'Maven 3.8.1'  // Ensure 'Maven 3.8.1' is correctly configured in Jenkins
    }
    stages {
        stage('Declarative: Checkout SCM') {
            agent { label 'master' }
            steps {
                git 'https://github.com/Arshiyapeerzade/demo.git'
            }
        }
        stage('Clone Repository') {
            agent { label 'master' }
            steps {
                deleteDir()
                git 'https://github.com/Arshiyapeerzade/demo.git'
            }
        }
        stage('Build on Slave 1') {
            agent { label 'slave-1' }
            environment {
                JAVA_HOME = tool name: 'JDK 17', type: 'jdk'
            }
            steps {
                sh "${env.JAVA_HOME}/bin/java -version"  // Verify Java version
                sh 'mvn clean compile package'
            }
        }
        stage('Test on Slave 2') {
            agent { label 'slave-2' }
            environment {
                JAVA_HOME = tool name: 'JDK 17', type: 'jdk'
            }
            steps {
                sh "${env.JAVA_HOME}/bin/java -version"  // Verify Java version
                sh 'mvn test'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
