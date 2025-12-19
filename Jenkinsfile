pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {
        stage('Git Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                dir('POV-JAVA') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('Create Docker Image') {
            steps {
                dir('POV-JAVA') {
                    bat 'docker build -t wadii/pos .'
                }
            }
        }

        stage('Run') {
            steps {
                bat 'docker run --name test-pos -d -p 8585:8282 wadii/pos'
            }
        }
    }
}
