pipeline {
    agent any
    options {
        checkoutToSubdirectory('src')
        buildDiscarder(logRotator(numToKeepStr: '14'))
    }
    environment{
        //def job params go here
        def github = 'kostovski'
        def gitUrl = 'https://github.com/kostovski/jenkins_test.git'
    }
    stages {
        stage('Prepare Workspace') {
            steps {
                git credentialsId: 'kostovski_githab', url: 'https://github.com/kostovski/jenkins_test.git'
            }
        }
        stage('test') {
            steps {
                echo "Test"
            }
        }
    }
    post {
        cleanup {
            deleteDir()
        }
    }
}