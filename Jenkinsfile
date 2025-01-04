
@Library('my-shared-library@main') _  // Correct syntax

pipeline {
    agent { label 'Node3' }
    // triggers {
    //     // Trigger at midnight every day
    //     cron('*/2 * * * *')
    // }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps { 
                script {
                   pipelineAll.checkoutCode()
               }
            }
        }

        stage('Set up Java 17') {
            steps {
                 script {
                   pipelineAll.setupJava()
                 }
            }
        }

        stage('Set up Maven') {
            steps {
                 script {
                   pipelineAll.setupMaven()
                 }
            }
        }

        stage('Build with Maven') {
            steps {
                 script {
                   pipelineAll.buildProject()
                 }
            }
        }
        // stage('Configure Git') {
        //     steps {
        //         script {
        //             // Set global Git user.name and user.email
        //             sh 'git config --global user.name "SanjanaKrishn"'
        //             sh 'git config --global user.email "sanjanabn6@gmail.com"'
        //         }
        //     }
        // }
        // stage('Tag Build') {
        //     steps {
        //         script {
        //             def buildTag = "build-${env.BUILD_NUMBER}"
        //             tagBuild(buildTag, "Tagging build number ${env.BUILD_NUMBER}")
        //         }
        //     }
        // }
        stage('Upload Artifact') {
            steps {
                 script {
                   pipelineAll.uploadArtifact('target/petclinic-0.0.1-SNAPSHOT.jar')
                 }
            }
        }

        stage('Run Application') {
            steps {
                 script {
                   pipelineAll.runApplication()
                 }
            }
        }

        stage('Validate App is Running') {
            steps {
                 script {
                   pipelineAll.validateApp()
                 }
            }
        }

        stage('Gracefully Stop Spring Boot App') {
            steps {
                 script {
                   pipelineAll.stopApplication()
                 }
            }
        }
    }

    post {
        always {
             script {
                   pipelineAll.cleanup()
             }
        }
    }
}
