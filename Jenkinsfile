pipeline {
        agent any

        tools {
            // Install the Maven version configured as "M3" and add it to the path.
            maven "M3"
        }

        stages {
          stage('Checkout') {
                  steps {
                        git branch: 'main', url: 'https://github.com/PaulMercer1/lbg-hello-world-maven.git'
                  }
          }
          stage('Compile') {
              steps {
                 // Run Maven on a Unix agent.
                 sh "mvn clean compile"
                }
           }
          stage('Testing') {
                steps {
                 // Run Maven on a Unix agent.
                 sh "mvn test"
                }
            }
          stage('SonarQube') {
                environment {
                        scannerHome = tool 'sonarqube'
                }
                steps {
                        withSonarQubeEnv('sonar-qube-1') {
                                sh "mvn sonar:sonar \
                                        -Dsonar.projectKey=maven-jenkins-pipeline \
                                        -Dsonar.host.url=${scannerHome}"
                        }
                }
           }
          stage('Package') {
                steps {
                    // Run Maven on a Unix agent.
                    sh "mvn package"
                }
            }
        }
}
