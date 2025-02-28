pipeline {
    agent any

    stages {
        stage('GIT') {
            steps {
                git branch: 'master', url: 'https://github.com/firasbessalah/devops.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        /*
        stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=squ_b89f78b6e34a1e612085135b6784f32676ec1480 -Dsonar.skipTests=true'
            }
        }*/
  stage('MVN Nexus') {
            steps {
                sh 'mvn deploy -Dmaven.test.skip=true'
            }
        }

        
    }
}
