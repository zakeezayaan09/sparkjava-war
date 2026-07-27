pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "----------- Build Started -----------"
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'zakdemy-sonar-scanner'
            }

            steps {
                withSonarQubeEnv('zakdemy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
