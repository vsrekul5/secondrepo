pipeline {
    agent any
    parameters {
        string(name : 'VERSION', defaultValue: '', description: 'version to deploy on the production environment')
        choice(name:'VERSION', choices:['','1.1.0', '1.2.0', '1.3.0'], description:'choices values')
        booleanParam(name : 'executeTest', defaultValue: true, description: 'select the condition.....')
    }
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('admin-user')
    }

    stages {
        
        stage('Building') {
            steps {
                echo 'Building the software!'
                echo "Building the software! VERSION ${params.VERSION}"
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
                    params.executeTest == true
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
                echo "Deploying the software version ${params.VERSION}"
                                
            }
        }
    }  
}
