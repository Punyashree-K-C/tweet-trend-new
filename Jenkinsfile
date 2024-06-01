pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment {
        JAVA_HOME = '/usr/bin/java'  // Set this to the actual path of JDK 17
        PATH = "${JAVA_HOME}/bin:/opt/apache-maven-3.9.7/bin:${env.PATH}"
    }
    stages {
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
