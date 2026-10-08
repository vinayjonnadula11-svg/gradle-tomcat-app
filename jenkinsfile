pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Gradle Build') {
            steps {
                bat 'gradle clean war'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.war',
                                 fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                    copy /Y "build\\libs\\gradle-tomcat-app.war" "C:\\Tomcat\\apache-tomcat-11.0.22-windows-x64\\apache-tomcat-11.0.22\\webapps\\gradle-tomcat-app.war"
                '''
            }
        }
    }

    post {
        success {
            echo 'Application successfully deployed to Tomcat!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}