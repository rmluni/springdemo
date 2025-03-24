pipeline {
    agent any

    environment {
        // GitHub repository and branch details
        REPO_URL = 'https://github.com/rmluni/springdemo.git'
        BRANCH_NAME = 'main'
        JAR_FILE_PATH = 'C:\\Users\\ramdesai\\.jenkins\\workspace\\GitTest1\\target\\springdemo-0.0.1-SNAPSHOT.jar'
        SPRING_BOOT_PORT = '8081'  // Change this to your custom port
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the GitHub repository
                git branch: "${BRANCH_NAME}", url: "${REPO_URL}"
            }
        }

        stage('Build JAR with Maven') {
            steps {
                script {
                    // Build the project using Maven (or Gradle) and package the JAR
                    sh 'mvn clean package -DskipTests'  // For Maven-based projects
                    // Alternatively, if using Gradle:
                    // sh './gradlew build'
                }
            }
        }

        stage('Run JAR') {
            steps {
                echo 'Deploying the application...'
                // Run the JAR file using the 'java -jar' command in Windows
                bat """
                java -jar ${JAR_FILE_PATH} --server.port=${SPRING_BOOT_PORT}
                """
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
