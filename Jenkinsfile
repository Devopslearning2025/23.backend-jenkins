pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    // environment{
    //     def AppVersion = '' //variable declaration
    // }
    environment{
        dev appVersion = ''
    }
    stages {
        stage("read the version") {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "APplication version : $appVersion"
                }
            }
        }
        stage('install dependencies') {
            steps {
                sh """
                npm install
                echo $appVersion
                """
            }
        }
        stage('build') {
            steps {
                sh """
                ls -lrth
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