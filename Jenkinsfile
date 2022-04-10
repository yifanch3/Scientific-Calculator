pipeline {
    agent any // set agent by free

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven 'Default maven' // the maven defined in the jenkins maven installation

    }

    // stages to build the staff
    stages {
        // run static analysis 
        stage('SonarQube analysis') {
            def sonarqubeScannerHome = tool name: 'SonarQube Scanner'

            withSonarQubeEnv('SonarQube') {
                sh "${sonarqubeScannerHome}/bin/sonar-scanner"
            }
        }

        // build the staff using maven
        stage('Build & Static analysis') { 
            sh 'mvn -f ./Calculator/pom.xml -B -DskipTests clean package sonar:sonar' // notice the path here
        }

        // the build is complete, run the sonarcube


        // run the test on the project
        stage('Test') {
            steps {
                // notice we mention the path directly, the folder structure of this project is different
                // and we need to point out the exact test class here
                sh 'mvn -f ./Calculator/pom.xml -Dtest=CalculatorSpec test' 
            }
            post {
                always {
                    // junit './Calculator/target/surefire-reports/*.xml' // no idea why this one not work ...
                    junit '**/Calculator/target/surefire-reports/*.xml' // but force a search on the workspace scale with project prefix work
                }
            }
        }

    }

}