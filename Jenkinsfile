pipeline {
    agent any
    options {
        checkoutToSubdirectory('src')
        buildDiscarder(logRotator(numToKeepStr: '14'))
    }
    environment{
        //def job params go here
        def github = 'kostovski'
        def gitUrl = 'url-here'
    }
    stages {
        stage('Prepare Workspace') {
            steps {
                checkout([
        				$class: 'GitSCM',
        				branches: [[name: "master"]],
        				browser: [$class: 'Stash',repoUrl: gitUrl],
        				doGenerateSubmoduleConfigurations: false,
        				extensions: [
        					[
        						$class: 'SubmoduleOption',
        						disableSubmodules: false,
        						parentCredentials: false,
        						recursiveSubmodules: true,
        						reference: '',
        						trackingSubmodules: false
        					],
        					[
        					    $class: 'RelativeTargetDirectory',
                                relativeTargetDir: 'src'
                            ],
        					[$class: 'WipeWorkspace'],
        					[$class: 'CloneOption', depth: 2, noTags: false, reference: '', shallow: true]
        				],
        				submoduleCfg: [],
        				userRemoteConfigs: [[
        					credentialsId: github,
        					url: gitUrl
        			   ]]
        			])
            }
        }
        stage('test') {
            steps {
                sh """echo $pwd
                """
            }
        }
    }
    post {
        cleanup {
            deleteDir()
        }
    }
}