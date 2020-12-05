pipeline {
    agent any
    tools {
        docker 'Docker'
    }
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