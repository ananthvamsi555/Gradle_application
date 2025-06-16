pipeline{
    agent any
    tool{
        gradle 'Gradle'
    }
    stages{
        stages("Check gradle version"){
            steps{
                script{
                    bat "\"${Gradle}\\bin\\gradle.bat\" --version"
                }

            }
        }
    }
}
