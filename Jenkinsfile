String PRETRONIC_CI_SSH_KEY_CREDENTIAL_ID = "1c1bd183-26c9-48aa-94ab-3fe4f0bb39ae"

String GIT_TEMPLATE_SSH = "git@github.com:Pretronic/Pretronic-Dokumentation-Template.git"

pipeline {
    agent any
    options {
        buildDiscarder logRotator(numToKeepStr: '10')
    }
    stages {
        stage('Install pip packages') {
            steps {
                script {
                    sh """
                    pip3 install --upgrade pip
                    pip3 install mkdocs-material

                    """
                }
            }
        }
        stage('Prepare directories') {
            steps {
                script {
                    sshagent([PRETRONIC_CI_SSH_KEY_CREDENTIAL_ID]) {
                        sh """
                        if [ -d "template" ]; then rm -Rf template; fi
                        mkdir template

                        if [ -d "build" ]; then rm -Rf build; fi
                        mkdir build


                        cd template/
                        git clone --single-branch --branch master ${GIT_TEMPLATE_SSH}
                        """
                    }
                }
            }
        }
        stage('Merge template in projects') {
            steps {
                script {

                    dir('projects') {
                       def files = findFiles()

                       files.each{ file ->
                          if(file.directory) {
                            echo "This is directory: ${file.name} "
                            sh "cp ../template/Pretronic-Dokumentation-Template/* ${file.name}/ -r"
                          }
                       }
                     }
                }
            }
        }
        stage("Build mkdocs") {
            steps {
                script {
                    sh """
                    for d in projects/ ; do
                        echo "$d"
                        ( cd $d ; mkdocs build )
                    done
                    """
                }
            }
        }
        stage("Move builds") {
            steps {
                script {
                    sh """
                    for d in projects/ ; do
                        mkdir build/$d
                        mv $d/* build/$d
                    done
                    """
                }
            }
        }
        stage("Push builds") {
            steps {
                script {
                    sh"""
                    git add build -v
                    git commit -m 'New mkdocs build' -- build -v
                    git push origin HEAD:main -v
                    """
                }
            }
        }
    }
}