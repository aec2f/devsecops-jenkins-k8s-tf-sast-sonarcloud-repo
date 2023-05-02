pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=aecudemy1 -Dsonar.organization=aectest -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=93118b4a89355487253ae022b50bce893068f765'
			}
        }
	   stage('RunSCAAnalysisUsingSnyk') {
		   steps { 
			   withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
			   	sh 'mvn snyk:test -fn'
			   }
		   }
	}   
  }
}
