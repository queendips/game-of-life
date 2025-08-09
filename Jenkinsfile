pipeline {
    agent any

    environment {
        MAVEN_HOME = "/opt/maven"
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/queendips/game-of-life.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Publish Test Reports') {
            steps {
                junit testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true, followSymlinks: false
            }
        }
    }

    post {
        success {
            mail to: 'gauriqueen2625@gmail.com',
                 subject: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Good news!

The Jenkins build for job *${env.JOB_NAME}* succeeded.

Details: ${env.BUILD_URL}
"""
        }

        failure {
            mail to: 'gauriqueen2625@gmail.com',
                 subject: "❌ Build FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Unfortunately, the Jenkins build for job *${env.JOB_NAME}* has failed.

Check console output: ${env.BUILD_URL}
"""
        }
    }
}
