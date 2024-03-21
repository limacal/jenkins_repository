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
                // Run the CodeCoverage Test only on the MAIN Branch.
                expression {
                    return env.BRANCH_NAME == 'main'
                }
            }
            steps {
                sh 'echo "Running CodeCoverage test"'
                // Run CodeCoverage test here (UNABLE TO RUN THE CODECOVERAGE)
               
            }
        }
        
        stage('Run Other Tests') {
            when {
                // Run other Tests on non-main Branches.
                not {
                    expression {
                        return env.BRANCH_NAME == 'main'
                    }
                }
            }
            steps {
                sh 'echo "Running other tests"'
                // Run other tests HERE.
            }
        }
        
        stage('Generate Jacoco Report') {
            when {
                expression {
                    // Generate Jacoco report on the main branch or if the build is successful.
                    return env.BRANCH_NAME == 'main' || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                // Generate Jacoco Report.
                sh 'echo "Generating Jacoco report"'
                // Include the command to generate Jacoco report here.
                
            }
            post {
                always {
                    // If tests fail, echo "tests fail!"
                    echo 'Tests FAIL!' // Assuming tests always pass for simplicity.
                    // If tests pass, echo "tests pass!"
                    echo 'Tests PASS!'
                }
            }
        }

        
        stage('Build and Test') {
            steps {
                // Execute build and test commands here
                sh 'mvn clean install' // Example Maven command
            }
        }


        
    }


    post {
        always {
            // Publish JaCoCo coverage reports
            jacoco(execPattern: '**/target/jacoco.exec')
            // You can specify multiple coverage report files by separating them with commas:
            // jacoco(execPattern: '**/target/jacoco.exec,**/other-path/jacoco.exec')
            }
        }
    
}
