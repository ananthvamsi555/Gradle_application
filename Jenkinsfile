@library('jenkins-shared-library') _
pipeline{
    agent any
    tools {
        gradle 'Gradle'
    }
    environment{
        URL = 'https://github.com/ananthvamsi555/Gradle_application.git'
        BRANCH = 'main'
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
                scmCheckout(REPO_URL,BRANCH_NAME)
            }
        }

    }
}
