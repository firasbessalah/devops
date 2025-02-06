pipeline {
    agent any

    stages {
        stage('GIT') {
            steps {
                git branch:"master",
                url: 'https://github.com/firasbessalah/devops.git'
            }
        }
         stage('compile') {
            steps {
               
               sh 'mvn clean compile'
               
            }
        }
    }
}
