pipeline{
    agent any
    tools {
        gradle 'Gradle'
    }
    stages {
        stage("Check gradle version"){
            steps{
                script{
                    bat "\"${Gradle}\\bin\\gradle.bat\" --version"
                }

            }
        }
    }
}
