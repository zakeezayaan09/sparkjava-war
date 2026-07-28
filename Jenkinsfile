pipeline {

    agent any

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {

        stage("build") {
            steps {
                echo "----------- build started ---------"

                sh 'mvn clean install -Dmaven.test.skip=true'

                echo "----------- build completed ---------"
            }
        }

        stage("test") {
            steps {
                echo "----------- unit test started ----------"

                sh 'mvn surefire-report:report'

                echo "---------- unit test completed ---------"
            }
        }

        stage("jar staging") {
            steps {
                echo "----------- jar staging started ----------"

                sh '''
                    # Create jarstaging directory in the workspace if it doesn't exist
                    mkdir -p jarstaging

                    # Copy built JAR file(s) from target directory into jarstaging
                    cp target/*.jar jarstaging/
                '''

                echo "---------- jar staging completed ---------"
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

    }

}
