pipeline {
    agent any

    environment {
        // You can specify the repository URL and the branch here
        REPO_URL = 'https://github.com/rmluni/springdemo.git'
        BRANCH_NAME = 'main'
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

        stage('Run Tests') {
            steps {
                script {
                    // Run unit tests (optional but recommended)
                    //sh 'mvn test'
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

        // (Optional) Deploy step, if needed
        // stage('Deploy') {
        //     steps {
        //         script {
        //             // Deployment commands can be placed here (e.g., copy JAR to a server or deploy to cloud)
        //             echo 'Deploying application'
        //         }
        //     }
        // }
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
