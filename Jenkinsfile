pipeline {
    agent any // set agent by free

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven 'Default maven' // the maven defined in the jenkins maven installation
    }

    // stages to build the staff
    stages {
        // build the staff using maven
        stage('Build') { 
            steps {
                sh 'mvn -f ./Calculator/pom.xml -B -DskipTests clean package' // notice the path here
            }
        }

        // run the test on the project
        stage('Test') {
            steps {
                // notice we mention the path directly, the folder structure of this project is different
                // and we need to point out the exact test class here
                sh 'mvn -f ./Calculator/pom.xml -Dtest=CalculatorSpec test' 
            }
            post {
                always {
                    junit './Calculator/target/surefire-reports/*.xml'
                }
            }
        }

    }

}