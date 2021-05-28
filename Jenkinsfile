pipeline {
    agent any
    
    options {
        ansiColor("xterm")
    }

    environment {
        GREEN="\033[32m"
        END="\033[0m"

        BRANCH="env.GIT_BRANCH"
    }

    stages {

        stage("Checkout stage") {
            steps {
                git(url: "https://opendev.org/jjb/jenkins-job-builder.git")
                sh "ls -l"
            }
        }

        stage("Test stage") {
            steps {
                echo "${GREEN}Run unit tests${END}\n"
                sh "tox -e py27"
            }
        }

        stage("Docs stage") {
            steps {
                echo "${GREEN}Run docs build${END}\n"
                sh "tox -e docs"
            }
        }

        stage("Coverage stage") {
            steps {
                echo "${GREEN}Run coverage build${END}\n"
                sh "tox -e cover"
            }
        }

        stage("Packaging stage") {
            steps {
                echo "${GREEN}Build python package${END}\n"
                sh "python setup.py bdist_wheel"
            }
        }
        
    }

    post {
        success {
            echo "${GREEN}FINISH OF PIPELINE${END}\n"
            archiveArtifacts("doc/source/*.rst")
        }
    }
}