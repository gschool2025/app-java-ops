pipeline {
    agent any
    parameters {
        tool { 
            jdk 'Java'
        }
        environment {
            JAVA_HOME = tool 'Java'
        }
    }
    stages {
        // Checkout stage: Download the source code from GitHub
        stage('Checkout') {
            steps {
                git url: 'https://github.com/gschool2025/app-java.git', branch: 'main'
            }
        }

        // Compile stage: Create build/classes directory and compile Main.java
        stage('Compile') {
            steps {
                // Create the build/classes directory if it doesn't exist
                script {
                    def buildDir = 'build/classes'
                    if (!fileExists(buildDir)) {
                        sh "mkdir -p ${buildDir}"
                    }
                }
                // Compile the Main.java file
                bat '"%JAVA_HOME%\\bin\\javac" -d build\\classes Main.java'
            }
        }

        // Prepare Manifest stage: Create a manifest file
        stage('Prepare Manifest') {
            steps {
                script {
                    def manifestFile = 'build/classes/META-INF/MANIFEST.MF'
                    def manifestDir = 'build/classes/META-INF'
                    // Create META-INF directory if it doesn't exist
                    if (!fileExists(manifestDir)) {
                        sh "mkdir -p ${manifestDir}"
                    }
                    // Create the manifest file with the Main-Class entry
                    writeFile file: manifestFile, text: "Main-Class: Main\n"
                }
            }
        }

        // Package stage: Package the compiled classes and the manifest into a JAR file
        stage('Package') {
            steps {
                script {
                    def jarDir = 'build/jar'
                    // Create the directory for the JAR file if it doesn't exist
                    if (!fileExists(jarDir)) {
                        sh "mkdir -p ${jarDir}"
                    }
                    // Package the classes and manifest into a JAR file
                    bat '"%JAVA_HOME%\\bin\\jar" cfe build/jar/MyApplication.jar Main -C build/classes .'
                }
            }
        }

        // Run stage: Run the application from the JAR file
        stage('Run') {
            steps {
                bat '"%JAVA_HOME%\\bin\\java" -jar build/jar/MyApplication.jar'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
