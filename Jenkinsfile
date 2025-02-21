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
stage('MVN SONARQUBE') {
    steps {
        sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=25175009@fifaF -Dsonar.skipTests=true'
    }
}

}
