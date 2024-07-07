pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    stages {
        stage ('read the version') {
            steps {
                def packageJson = readJSON file: 'package.json'
                def AppVersion = packageJson.version
                echo "application version is $AppVersion"
            }

        }
        stage('install dependencies') {
            steps {
                sh """
                npm install
                ls -lrth 
                echo $AppVersion
                """
            }
        }
    }  
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success {
            echo 'i will run the pipeline is usccess'
        }
        failure {
            echo 'i will the pipeline is failure'
        }
    }
}