pipeline {
    agent any // set agent by free

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven 'Default maven' // the maven defined in the jenkins maven installation

    }

    // stages to build the staff
    stages {

        // build the staff using maven first
        stage('Build') { 
            steps {
                sh 'mvn -f ./Calculator/pom.xml -B -DskipTests clean package' // notice the path here
            }
        }


        // then run static analysis 
        stage('Sonar analysis') {
            environment {
                SCANNER_HOME = tool 'SonarQubeScanner'
                ORGANIZATION = "yifanch3_HW3"
                PROJECT_NAME = "yifanch3_HW3_code"
            }
            steps {
                withSonarQubeEnv('LocalSonarCloud') {
                    sh 'pwd'
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                    -Dsonar.java.binaries=./Calculator/target/classes/io/michaelcane \
                    -Dsonar.projectKey=$PROJECT_NAME \
                    -Dsonar.sources=.'''
                }
            }
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