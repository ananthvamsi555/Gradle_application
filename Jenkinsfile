@Library('jenkins-shared-library') _
pipeline{
    agent any
    tools {
        gradle 'Gradle'
    }
    environment{
        repoUrl = 'https://github.com/ananthvamsi555/Gradle_application.git'
        branch = 'main'
    }
    stages {
        stage("Check gradle version"){
            steps{
                script{
                    def gradleHome = tool name: 'Gradle', type: 'hudson.plugins.gradle.GradleInstallation'
                    bat "\"${gradleHome}\\bin\\gradle.bat\" --version"
                }

            }
        }
        stage("Checkout"){
            steps{
                scmCheckout(repoUrl,branch)
            }
        }
        stage("Build"){
            steps{
                bat 'gradlew.bat clean build'
            }
        }
        stage('Publish to Nexus') {
            environment {
                // Inject Nexus credentials only in this stage
                NEXUS = credentials('nexus-creds')
            }
            steps {
                bat 'gradlew.bat publish -PnexusUser=%NEXUS_USR% -PnexusPassword=%NEXUS_PSW%'
            }
        }

    }
}
