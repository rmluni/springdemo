pipeline {
    agent any

    environment {
        // GitHub repository and branch details
        REPO_URL = 'https://github.com/rmluni/springdemo.git'
        BRANCH_NAME = 'main'
        JAR_FILE_NAME = 'your-application.jar'  // Replace with your actual JAR file name
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

        stage('Run JAR from GitHub') {
            steps {
                script {
                    // Construct the URL to the JAR file in the GitHub repository
                    def jarFileUrl = "https://raw.githubusercontent.com/rmluni/springdemo/${BRANCH_NAME}/target/${JAR_FILE_NAME}"
                    echo "JAR file URL: ${jarFileUrl}"

                    // Use wget or curl to download the JAR file directly from GitHub (if required)
                    sh """
                    curl -L -o ${JAR_FILE_NAME} ${jarFileUrl}
                    """

                    // Run the downloaded JAR file (in the same pipeline)
                    sh "java -jar ${JAR_FILE_NAME}"
                }
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
