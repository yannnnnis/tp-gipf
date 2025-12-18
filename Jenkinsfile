node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    withSonarQubeEnv() {
      sh "./gradlew sonar"
    }
  }
}
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './gradlew -D https.proxyHost=proxy1-rech -D https.proxyPort=3128 compileJava'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew -D https.proxyHost=proxy1-rech -D https.proxyPort=3128 test'
            }
        }
        stage('Sonar') {
            steps {
                sh "./gradlew -D https.proxyHost=proxy1-rech -D https.proxyPort=3128 sonar -Dsonar.projectKey=tp-gipf -Dsonar.projectName='tp-gipf' -Dsonar.host.url=http://172.17.0.1:9000 -Dsonar.token=sqp_8ed37c4fb23351cf619c21e27eafb27610036624"
            }
        }
        stage('Jar') {
            steps {
                sh "./gradlew -D https.proxyHost=proxy1-rech -D https.proxyPort=3128 jar"
            }
        }
    }
}
