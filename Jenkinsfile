pipeline {
    agent { label 'docker' } // Run on the slave node
    tools{
        maven 'maven3'
    }
    environment {
        MAVEN_VERSION = '3.9.5'
        MAVEN_HOME = '/opt/maven'
        PATH = "${MAVEN_HOME}/bin:${PATH}"
    }

    //environment {
        // Use Jenkins credentials for secure access
        //GITHUB_CREDENTIALS = credentials('github-credentials-id')  mvn -f path/to/pom.xml
        //}

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the branch
                git branch: 'master',
                    credentialsId: 'github-credentials-id',
                    url: 'https://github.com/nikuser2021/maven-web-app.git' // Replace with your repo URL
            }
        }
        stage('Compile') {
            steps {
                script {
                    echo 'Building the application...'
                    
                    // Compile the application
                    //sh 'mvn -f simple-springboot-app/pom.xml'
                    sh "mvn clean compile"
                    
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    // Add your build commands here
                    sh "mvn package"
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    // Add your test commands here
                    sh "mvn test" // Example for Gradle tests
                }
            }
        }
    }
    post {
        success {
            slackSend(channel: '#jk', message: "Build Successful: ${env.JOB_NAME} - ${env.BUILD_NUMBER}")
        }
        failure {
            slackSend(channel: '#jk', message: "Build Failed: ${env.JOB_NAME} - ${env.BUILD_NUMBER}")
        }
    }
}






