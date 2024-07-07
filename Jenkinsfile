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
        stage('install dependencies') {
            steps {
                sh """
                dnf install nodejs -y
                npm install
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