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
                            sh "mvn clean test -P h2"
                        }
                   }
                   stage('SonarQube Analysis') {
                        steps {
                            withSonarQubeEnv('SonarQube') {
                                sh 'mvn sonar:sonar'
                            }
                        }
                   }
                   stage('Build Jars') {
                       steps {
                           echo "Building jar...!"
                           sh 'mvn clean package'
                       }
                   }
                   stage("Deploy with Ansible") {
                        steps {
                          echo "Ansible Playbook......!"
                          sh "ansible-playbook playbook.yml -i inventory.ini --private-key  /var/lib/jenkins/credentials/keywebJG.pem"
                        }
                   }

         }
}
