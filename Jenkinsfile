pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=aectest -Dsonar.organization=aectest -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=588feb83a6ded5998109417e5f8df788aacae3e3'
			}
        } 
  }
}
