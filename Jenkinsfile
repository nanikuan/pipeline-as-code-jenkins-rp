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
        
        
        stage('Stage 1-21051176') {
            steps {
                sh """
                echo "Stage 1 completed - 21051176"
                """
            }
        }
        

        stage('Stage 2-21051176'){
            parallel {
                stage('Execute Shell'){
                    steps{
                    sh """
                    echo "Stage 2 completed - 21051176"
                    """                    
                    }
                }
                 stage('Create Container'){
                    steps{
                        sh 'docker run --detach -it --name=apche2-21051176-container4 apcahe2-21051176-image2 /bin/bash'
                        
                    }
                }

            }
        }
        stage('Stage 3-21051176') {
            steps {
                sh """
                echo "Stage 3 completed - 21051176"
                """
            }
        }
        stage('Stage 4-21051176') {
            steps {
                input('Proceed to release the work?')
            }
        }
        
        stage('Stage 5-21051176') {

            steps {
                sh """
                echo "work released - 21051176"
                """
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
