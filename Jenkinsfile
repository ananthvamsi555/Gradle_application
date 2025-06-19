@Library('jenkins-shared-library') _

pipeline {
    agent any

    tools {
        gradle 'Gradle'
    }

    environment {
        repoUrl = 'https://github.com/ananthvamsi555/Gradle_application.git'
        branch  = 'main'
    }

    stages {

        stage("Check Gradle Version") {
            steps {
                script {
                    def gradleHome = tool name: 'Gradle', type: 'hudson.plugins.gradle.GradleInstallation'
                    bat "\"${gradleHome}\\bin\\gradle.bat\" --version"
                }
            }
        }

        stage("Checkout") {
            steps {
                scmCheckout(repoUrl, branch)
            }
        }

        stage("Build") {
            steps {
                bat 'gradlew.bat clean build'
            }
        }

        stage("Publish to Nexus") {
            environment {
                NEXUS_URL = "http://localhost:8082/repository/maven-releases/"
                NEXUS_CREDENTIALS_ID = "nexus-creds" // Create this in Jenkins → Manage Credentials
            }
            steps {
                script {
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: 'localhost:8082',
                        groupId: 'TEST',
                        version: '1.0.0',
                        repository: 'maven-releases',
                        credentialsId: "${NEXUS_CREDENTIALS_ID}",
                        artifacts: [[
                            artifactId: 'Gradle_Application', 
                            classifier: '', 
                            file: 'build\\libs\\Gradle_Application-1.0.0.jar', 
                            type: 'jar'
                        ]]
                    )
                }
            }
        }
    }
}
