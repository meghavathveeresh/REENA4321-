pipeline {
    agent any
 
    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'GITHUB', url: 'https://github.com/meghavathveeresh/shannu-dev.git'
            }
        }
          stage('Build') {
            steps {
               bat 'mvn clean install'
            }
        }
	    stage('Test') {
            steps {
               bat 'mvn test'
            }
        }
          stage('Generate Artifacts') {
            steps {
               archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
        }
		stage('Deploy to Tomcat Server') {
        steps {
           deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'AMDN', path: '', url: 'http://localhost:8080/')], contextPath: 'shannudev', war: 'target/*.war'
        }
    }
    }
}
