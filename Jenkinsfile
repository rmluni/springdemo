pipeline {
    agent any

    environment {
        // Define the JAR file name and path
        JAR_FILE = 'target/springdemo-0.0.1-SNAPSHOT.jar' // Replace with the correct JAR file name
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository to Jenkins workspace
                git 'https://github.com/rmluni/springdemo.git' // Replace with your GitHub repo URL
            }
        }

        stage('Build JAR') {
            steps {
                script {
                    // Use Maven to build the project (or Gradle if you're using that)
                    sh 'mvn clean package -DskipTests'  // For Maven-based projects
                    // Or, for Gradle projects:
                    // sh './gradlew build'
                }
            }
        }

        stage('Run JAR') {
            steps {
                script {
                    // Ensure the JAR file exists and run it
                    if (fileExists(JAR_FILE)) {
                        echo "Running JAR file: ${JAR_FILE}"
                        sh "java -jar ${JAR_FILE}"
                    } else {
                        error "JAR file does not exist at ${JAR_FILE}"
                    }
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
