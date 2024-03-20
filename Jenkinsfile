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
                branch 'main'
            }
            steps {
                sh 'echo "Running CodeCoverage test"'
                // Run CodeCoverage test here
                echo "This is the MAIN Branch"
            }
        }
        
        stage('Run Other Tests') {
            when {
                // Run other tests on non-main branches
                not {
                    branch 'branch_1'
                }
            }
            steps {
                sh 'echo "Running other tests"'
                // Run other tests here
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

          stage("Tests") {
		      try {
                    sh '''
        	        pwd
               		cd Chapter08/sample1
                    ./gradlew test
                    ./gradlew jacocoTestReport
                    '''
                    } catch (Exception E) {
                        echo 'Failure detected'
                    }
                    // from the HTML publisher plugin
                    // https://www.jenkins.io/doc/pipeline/steps/htmlpublisher/
                    publishHTML (target: [
                       //reportDir: 'Chapter08/sample1/build/reports/tests/test',
                       reportDir: 'https://github.com/limacal/jenkins_repository/test'
                       reportFiles: 'index.html',
                       reportName: "JaCoCo Report"
                    ])                       
          }
    }
}
