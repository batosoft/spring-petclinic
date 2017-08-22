pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './mvnw spring-boot:run' 
            }
        }
        stage('Test') {
            steps {
                sh 'make check || true' 
                junit './src/test/jmeter/petclinic_test_plan.jmx' 
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                sh 'make publish'
            }
        }
    }
}
