#!groovy

pipeline {
    agent {
        docker { image 'python:3' }
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
    post {
        success {

        }
    }
}