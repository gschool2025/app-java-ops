pipeline {
    agent any
    parameters {

        tool { 
            jdk 'Java'
        }

        environment  {
            JAVA_HOME = tool 'Java'
        }

        stages {
            stage('Checkout') {
                steps {
                    git url: 'https://github.com/gschool2025/app-java.git', branch: 'main'
                }
        }

        stage('Compile') {
            steps {
                bat '"%JAVA_HOME%\\bin\\javac" -d build\\classes Main.java'
}
