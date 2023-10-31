pipeline {
        agent any

        tools {
            // Install the Maven version configured as "M3" and add it to the path.
            maven "M3"
        }

        stages {
            stage('Checkout') {
                steps {
                    // Get some code from a GitHub repository

                    git branch: 'main', url: 'https://github.com/LoudShadow/lbg-hello-world-maven.git'
                }
            }
            stage("SonarQube"){
                environment {
                        scannerHome = tool "sonarqube"
                }
                steps{
                    withSonarQubeEnv("sonar-qube-1"){
                        sh "$(scannerHome)/bin/sonar-scanner"
                   }
                        
                }
            }
            stage('Compile') {
                steps {
                    // Run Maven on a Unix agent.
                    sh "mvn clean compile"
                }
            }
        }
}
