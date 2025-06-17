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
                NEXUS = credentials('nexus-creds')
            }
            steps {
                script {
                    def buildVersion = "1.0.${env.BUILD_NUMBER}"
                    bat "gradlew.bat publish -PnexusUser=%NEXUS_USR% -PnexusPassword=%NEXUS_PSW% -PbuildVersion=${buildVersion}"
                    echo "Build version ${buildVersion}"
                }
            }
        }
    }
}
