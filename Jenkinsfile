pipeline {
    agent any
    parameters {
        booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Czy uruchomić etap wdrożenia?')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building applications...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing Applications...'
            }
        }
        stage('Deploy') {
            when {
                expression { params.DEPLOY }
            }
            steps {
                echo 'Implementing applications...'
            }
        }
    }
}
