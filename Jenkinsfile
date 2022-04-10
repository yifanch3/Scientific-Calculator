pipeline {
    agent any // set agent by free

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3" // install the right maven version here
    }

    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}