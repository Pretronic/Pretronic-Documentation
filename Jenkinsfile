final String PRETRONIC_CI_SSH_KEY_CREDENTIAL_ID = "1c1bd183-26c9-48aa-94ab-3fe4f0bb39ae"

final String GIT_TEMPLATE_SSH = "git@github.com:Pretronic/Pretronic-Dokumentation-Template.git"

final String GIT_DOCS_SSH = "git@github.com:Pretronic/Pretronic-Documentation.git"

final String CI_NAME = "PretronicCI"
final String CI_EMAIL = "ci@pretronic.net"

final String CNAME = "docs.pretronic.net"

final String PROJECT_NAME = "Pretronic-Documentation"
final String TEMPLATE_PROJECT_NAME = "Pretronic-Dokumentation-Template"

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
                    pip3 install mkdocs-material
                    pip install mkdocs-git-revision-date-plugin
                    pip install mkdocs-git-committers-plugin-2
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
                            sh "cp ../template/${TEMPLATE_PROJECT_NAME}/* ${file.name}/ -r -n"
                          }
                       }
                     }
                }
            }
        }
        stage("Build mkdocs") {
            steps {
                script {
                    dir('projects') {
                       def files = findFiles()

                       files.each{ file ->
                          if(file.directory) {
                            sh "cd ${file.name} && mkdocs build"
                          }
                       }
                     }
                }
            }
        }
        stage("Deploy builds") {
            steps {
                script {
                    sshagent([PRETRONIC_CI_SSH_KEY_CREDENTIAL_ID]) {
                        sh """
                        git config --global user.name '$CI_NAME' -v
                        git config --global user.email '$CI_EMAIL' -v
                        """

                        sh """
                        cd build/
                        git clone --single-branch --branch gh-pages ${GIT_DOCS_SSH}
                        cd ${PROJECT_NAME}/
                        rm -R ./*
                        echo ${CNAME} > CNAME
                        """
                        dir('projects') {
                           def files = findFiles()

                           files.each{ file ->
                              if(file.directory) {
                                sh "mkdir ../build/${PROJECT_NAME}/${file.name} && cp ${file.name}/site/* ../build/${PROJECT_NAME}/${file.name}/ -r"
                              }
                           }
                         }
                        sh """
                        cd build/${PROJECT_NAME}/
                        cp home/* ./ -r
                        rm -R home/
                        git add . -v
                        git commit -m 'New mkdocs build' -v
                        git push origin HEAD:gh-pages -v
                        """
                    }
                }
            }
        }
    }
}
