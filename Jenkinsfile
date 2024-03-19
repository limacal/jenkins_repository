pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Run Tests') {
            when {
                // Run CodeCoverage test only on the main branch
                branch 'branch_2'
            }
            steps {
                sh 'echo "Running CodeCoverage test"'
                // Run CodeCoverage test here
                echo "This is the BRANCH_2 Branch"
            }
        }

        stage('Generate Jacoco Report') {
            steps {
                // Generate Jacoco report
                sh 'echo "Generating Jacoco report"'
                // Include the command to generate Jacoco report here
                echo "This is the Jacoco Report"
                
            }
            post {
                always {
                    // If tests fail, echo "tests fail!"
                    echo 'TESTS FAILED!'
                    // If tests pass, echo "tests pass!"
                    echo 'TESTS PASSED!'
                    
                }
            }
        }
    }
}
