pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.7/bin:$PATH"
}
    stages {
        stage("build"){
            steps {
                sh 'mvn clean deploy -DskipTests'
            }
        }
        stage('SonarQube analysis') {
    tools {
        jdk "jdk17" // the name you have given the JDK installation in Global Tool Configuration
    }
    environment {
        scannerHome = tool 'sripavan-sonar-scanner' // the name you have given the Sonar Scanner (in Global Tool Configuration)
    }
    steps {
        withSonarQubeEnv(installationName: 'sripavan-sonarqube-server') {
            sh "${scannerHome}/bin/sonar-scanner -X"
        }
    }
    }
}
}