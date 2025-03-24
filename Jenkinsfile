pipeline {
    agent any

    environment {
        // You can specify the repository URL and the branch here
        REPO_URL = 'https://github.com/rmluni/springdemo.git'
        BRANCH_NAME = 'main'
        JAR_FILE_NAME = 'springdemo-0.0.1-SNAPSHOT.jar' 
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git branch: "${BRANCH_NAME}", url: "${REPO_URL}"
            }
        }

        stage('Build with Maven') {
            steps {
                script {
                    // Run Maven clean and package command to build the project
                    // This assumes that Maven is installed and properly configured on your Jenkins agent
                    sh 'mvn clean package -DskipTests'  // Skipping tests for faster build (can be changed)
                }
            }
        }

        stage('Build Artifact') {
            steps {
                script {
                    // If the build is successful, package the project into a JAR/WAR file
                    // Maven stores the artifact in the target folder by default
                    echo "The JAR/WAR file is built in the target directory."
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
            echo "Build completed successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}