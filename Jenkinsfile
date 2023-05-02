pipeline {
  agent any
  tools {
      maven 'Maven_3_5_2'
  }
  stages {
    stage('CompileandRunSonarAnalysis') {
      steps {
        /* groovylint-disable-next-line LineLength */
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
    stage('Build') {
      steps {
        withDockerRegistry([credentialsId: 'dockerlogin', url: '']) {
          script {
            app = docker.build('aec2fasg')
          }
        }
      }
    }
    stage('Push') {
      steps {
        script {
          docker.withRegistry('https://281157408708.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-2:aws-credentials') {
            app.push('latest')
          }
        }
      }
    }
    stage('Kubernetes Deployment of ASG Bugg Web Application') {
      steps {
        withKubeConfig([credentialsId: 'kubelogin']) {
          sh('kubectl delete all --all -n devsecops')
          sh('kubectl apply -f deployment.yaml --namespace=devsecops')
        }
      }
    }
  }
}
