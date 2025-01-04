@Library('my-shared-library@main') _
pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('pipeline') {
            steps {
                pipeline()
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Any cleanup steps, like stopping the app or cleaning up the environment
            sh 'pkill -f "mvn spring-boot:run" || true' // Ensure the app is stopped
        }
    }
}
