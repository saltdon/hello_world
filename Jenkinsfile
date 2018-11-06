pipeline {
    agent none
    stages {
        stage('Build') {
            agent any
            steps {
                checkout scm
                sh 'make'
                stash includes: '**/target/*.jar', name: 'app' (1)
            }
        }
        stage('Test on Linux') {
            agent { (2)
                label 'linux'
            }
            steps {
                unstash 'app' (3)
                sh 'make check'
            }
            post {
                always {
                    junit '**/target/*.xml'
                }
            }
        }
        stage('Test on Windows') {
            agent {
                label 'windows'
            }
            steps {
                unstash 'app'
                bat 'make check' (4)
            }
            post {
                always {
                    junit '**/target/*.xml'
                }
            }
        }
    }
}}  }
