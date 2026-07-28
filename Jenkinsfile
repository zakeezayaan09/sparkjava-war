pipeline {

    agent any

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {

        stage("build") {
            steps {
                echo "----------- build started ---------"

               // sh 'mvn clean deploy -Dmaven.test.skip=true'

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

stage('Stage JAR') {
    steps {
        sh '''
            # Create the folder in the workspace
            mkdir -p jarstaging

            # Copy the built JAR file from target into jarstaging
            cp target/*.jar jarstaging/
        '''
    }
}
