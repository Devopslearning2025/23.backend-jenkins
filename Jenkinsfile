pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment {
        def appVersion = '' //variable declaration
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
                zip -q -r backend-${appVersion}.zip * -x Jenkinsfile -x backend-${appVersion}.zip
                ls -lrth
                """
            }
        }    
    environment{
        nexusUrl = http://3.81.33.200:8081/repository
    }

        }
        stage('Nexus Artifact upload') {
            steps {
                script {
                     nexusArtifactUploader(
                            nexusVersion: 'nexus3',
                            protocol: 'http',
                            nexusUrl: "${nexusUrl}",
                            groupId: 'com.expense',
                            version: version,
                            repository: 'backend',
                            credentialsId: 'nexus-auth',
                            artifacts: [
                                [artifactId: "backend",
                                classifier: '',
                                file: "backend-" + "${appVersion}" + ".zip",
                                type: 'zip']
                            ]
                    )
                }
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