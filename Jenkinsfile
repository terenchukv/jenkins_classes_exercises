pipeline {
    agent any

    stages {

        stage("Checkout") {
            steps {
                git(url: "https://opendev.org/jjb/jenkins-job-builder.git")
            }
        }

        stage("Listing stage") {
            steps {
                sh "ls -l"
            }
        }

        stage("Test stage") {
            steps {
                sh "tox -e py27"
            }
        }

        stage("Docs stage") {
            steps {
                sh "tox -e docs"
            }
        }

        stage("Coverage stage") {
            steps {
                sh "tox -e cover"
            }
        }

        stage("Packaging stage") {
            steps {
                sh "python setup.py bdist_wheel"
            }
        }
        
    }

    post {
        success {
            echo "Finish of pipeline"
        }
    }
}