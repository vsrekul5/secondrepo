pipeline {
    agent any
    parameters {
        string(name : 'VERSION', DefaultValue: '', description: 'version to deploy on the production env')
        choice(name:'VERSION', choices:['1.1.0', '1.2.0', '1.3.0'], description:'')
        booleanParam(name : 'executeTest', DefaultValue: true, description: 'select the condition.....')
    }
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('admin-user')
    }

    stages {
        
        stage('Building') {
            steps {
                echo 'Building the software!'
                echo "Building the software! VERSION ${NEW_VERSION}"
            }
        }
        stage('Artifact Archiving') {
            steps {
                echo 'The Artifact will be uploaded to an artifact repository'
            }
        }
        stage('Testing') { 
            when {
                expression {
                    param.executeTest == true
                }
            }
            steps {
                echo 'Testing the software!'
            }
        }
        stage('Staging') {
            steps {
                echo 'The Artifact is staged onto the staging server'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying the software!'
                echo "running scripts ${SERVER_CREDENTIALS}"
                echo "Deploying the software version ${params.VERSION}"
                sh "${SERVER_CREDENTIALS}"
                withCredentials([
                    userNamePassword(credentials: 'admin-user', userNameVariable: user, userPasswordVariable: pwd)
                ]){
                  sh "Deploying the software! ${user} ${pwd}"
                }
            }
        }
    }  
}
