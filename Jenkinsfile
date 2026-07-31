pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {

        stage("build") {
            steps {
                sh 'mvn clean install'
            }

        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'zakdemy-sonar-scanner'


            }

            steps {
                withSonarQubeEnv('zakdemy-sonarqube-server') {

                    sh "${scannerHome}/bin/sonar-scanner"

                }
            }
        }

