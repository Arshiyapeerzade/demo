pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                deleteDir()
                git 'https://github.com/Arshiyapeerzade/demo.git'
            }
        }
        
        stage('Build on Slave 1') {
            agent {
                label 'slave-1'
            }
            steps {
                echo 'Building on slave-1 node'
                sh '/usr/share/maven/bin/mvn clean compile package'
            }
        }
        
        stage('Test on Slave 2') {
            agent {
                label 'slave-2'
            }
            steps {
                sh '/usr/share/maven/bin/mvn test'
            }
        }
    }
    
    post {
        always {
            deleteDir()
        }
    }
}
