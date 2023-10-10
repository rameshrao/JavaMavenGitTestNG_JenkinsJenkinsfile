pipeline {
    agent any
    tools { 
        maven 'Maven' 
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
            post {
            	always{
            	    junit 'target/surefire-reports/*.xml'
            	}
            }
        }
        stage('Result') {
            steps {
                echo "Result Started"
                step([$class: 'Publisher', reportFilenamePattern: '**/testng-results.xml'])
                echo "Result End"
            }
        }
        stage('Install') {
            steps {
                echo "Install Started"
                sh(/mvn -file pom.xml install/)
                echo "Install End"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy Started"
                sh(/mvn -file pom.xml deploy/)
                echo "Deploy End"
            }
        }
    }
}