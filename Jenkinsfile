pipeline {

        agent any

        tools {
            // Install the Maven version configured as "MAVEN_HOME" and add it to the path
            maven "MAVEN_HOME"
        }

        stages {
                   stage('Build') {
                        steps {
                            echo "Building....!"
                            sh 'mvn clean compile'
                        }
                   }
                   stage('Test') {
                        steps {
                            echo "Running tests"
                            sh "mvn clean test"
                        }
                   }
                   stage('SonarQube Analysis') {
                        steps {
                            withSonarQubeEnv('SonarQube') {
                                sh 'mvn sonar:sonar'
                            }
                        }
                   }
         }
}
