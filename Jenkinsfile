pipeline {
    agent any
    tools { 
        maven 'Maven 3.9.4' 
        jdk 'JDK 17' 
    }
    stages {
        stage('Clean') {
            steps {
                echo "Clean Start"
                sh(/mvn -file pom.xml clean/)
                echo "Clean End"
            }
        }
        stage('Compile') {
            steps {
                echo "Code Compilation Started"
                sh(/mvn -file pom.xml compile/)
                echo "Code Compilation End"
            }
        }
        stage('Test') {
            steps {
                echo "Test Started"
                sh(/mvn -file pom.xml test/)
                echo "Test End"
            }
            echo "Post result"
            post {
            	always{
            	    junit 'target/surefire-reports/*.xml'
            	}
            }
            echo "Post result completed"                
        }
        stage('Result') {
            steps {
                echo "Result Started"
                junit '**/test-output/emailable-report.html'
                echo "Result End"
            }
        }
    }
}