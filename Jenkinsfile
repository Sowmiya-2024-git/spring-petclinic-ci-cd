pipeline {
    agent any

    tools {
        jdk 'Java 17'
        maven 'Maven 3'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Cloning Repository...'
                git 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Building the project...'
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                bat 'mvn test'
            }
        }

        stage('Code Coverage') {
            steps {
                echo '📈 Generating JaCoCo coverage report...'
                bat 'mvn verify'
            }
        }
    }

    post {
        success {
            echo '✅ Build and tests passed successfully!'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            echo '📦 Artifact archived successfully!'
        }
        failure {
            echo '❌ Build or tests failed!'
        }
        always {
            junit 'target/surefire-reports/*.xml'
            echo '📊 Test results archived.'
        }
    }
}
