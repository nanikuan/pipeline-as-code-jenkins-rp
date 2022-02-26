pipeline {

    agent {
        node {
            label 'master'
        }
    }

    tools { 
        maven 'maven3' 
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '15', 
                    numToKeepStr: '10'
            )
    }

    environment {
        APP_NAME = "STUDENT_APP"
        APP_ENV  = "DEV"
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace for ${APP_NAME}"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
                ])
            }
        }

        stage('Code Build') {
            steps {
                 sh 'mvn install -Dmaven.test.skip=true'
            }
        }

        stage('Stage 2-21051176'){
            parallel {
                stage('Create Container'){
                    steps{
                        sh 'docker run -d -it --name=stage2-21051176-container apache2-21051176-image /bin/bash'
                        
                    }
                }
                stage('Execute Shell'){
                    steps{
                    sh """
                    echo "Stage 2 completed - 21051176"
                    """                    
                    }
                }

            }
        }
        
        stage('Printing All Global Variables') {
            steps {
                sh """
                env
                """
            }
        }




    }   
}
