pipeline {
    agent any  // Use any available agent

    environment {
        // Set up environment variables
        NODE_HOME = tool 'NodeJS'  // Make sure NodeJS is configured in Jenkins
        PATH = "${NODE_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your repository
                git 'https://github.com/BasselZeidan80/PlayWrightFrameWork-Cucumber.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install project dependencies
                script {
                    sh 'npm install'  // Use 'bat' for Windows: bat 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run your regression tests
                script {
                    sh 'npm run regression'  // Adjust based on your testing needs
                }
            }
        }

        stage('Generate Report') {
            steps {
                // Generate the Cucumber report
                script {
                    sh 'npm run generate-report'  // Ensure this script is defined in package.json
                }
            }
        }

        stage('Archive Reports') {
            steps {
                // Archive the generated HTML report
                archiveArtifacts artifacts: 'reports/cucumber_report.html', fingerprint: true
            }
        }
    }

    post {
        success {
            // Actions to take on success
            echo 'Tests ran successfully!'
        }
        failure {
            // Actions to take on failure
            echo 'Tests failed. Check the logs.'
        }
    }
}
