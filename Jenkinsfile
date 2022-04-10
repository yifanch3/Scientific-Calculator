pipeline {
    agent any // set agent by free

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven 'Default maven' // the maven defined in the jenkins maven installation
    }

    // stages to build the staff
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -f ./Calculator/pom.xml -B -DskipTests clean package' 
            }
        }
    }


    stage('Test') {
        steps {
            sh 'mvn test'
        }
        post {
            always {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
}