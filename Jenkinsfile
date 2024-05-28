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
                echo "--------build started-------------------"
                sh 'mvn clean deploy -DskipTests'
                echo "--------build completed-------------------"
            }
        }
        // stage("test"){
        //     steps{
        //         echo "--------unit test started-------------------"
        //         sh 'mvn surefire-report:report'
        //         echo "--------unit test completed-------------------"
        //     }
        // }

        stage('SonarQube analysis') {
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