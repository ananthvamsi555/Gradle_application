pipeline{
    agent any
    tools {
        gradle 'Gradle'
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
    }
}
