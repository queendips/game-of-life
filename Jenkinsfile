pipeline {
    agent any

    environment {
        MAVEN_HOME = "/opt/maven"
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    tools {
        // Make sure these tool names match your Jenkins global tool configuration
        jdk 'corretto-1.8'    
        maven 'maven'         // Use the Maven installation name configured in Jenkins
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/queendips/game-of-life.git'
            }
        }

        stage('Build') {
            steps {
                // Build all modules, run tests in all modules
                sh 'mvn clean install'
            }
        }

        stage('Publish Test Reports') {
            steps {
                // Collect test reports from all modules
                junit '**/target/surefire-reports/*.xml', allowEmptyResults: true
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive jars from all modules, if any produced
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true, followSymlinks: false
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
