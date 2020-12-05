pipeline {
    agent any
    options {
        buildDiscarder logRotator(numToKeepStr: '10')
    }
    stages {
        stage('Test') {
            steps {
                script {
                    sh "pip --version"
                }
            }
        }
    }
}