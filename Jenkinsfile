pipeline {
    agent any

    environment {
        MAVEN_HOME = "/opt/maven"
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    tools {
        jdk 'corretto-1.8'
        maven 'maven-3.9.11'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/queendips/game-of-life.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Publish Test Reports') {
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true, followSymlinks: false
            }
        }
    }
}

