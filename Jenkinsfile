pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${JAVA_HOME}/bin:/opt/apache-maven-3.9.7/bin:${env.PATH}"
    }
    stages {
        stage('Verify Java Version') {
            steps {
                sh 'java -version'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean deploy'
            }
        }
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'galaxy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('galaxy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
