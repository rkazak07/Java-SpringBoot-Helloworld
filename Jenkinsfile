pipeline {

	environment {
	  dockerimagename = "rkazak1/springboot-hello1"
          dockerImage = ""
	}
	
  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/rkazak07/projects.git', branch:'main'
      }
    }
    
      stage("Build image") {
            steps {
                script {
		    
                    dockerImage = docker.build dockerimagename
                }
            }
        }
    
    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "values.yaml", kubeconfigId: "kubeconfig")
	  kubernetesDeploy(configs: "ingress.yml", kubeconfigId: "kubeconfig")
        }
      }
    }

  }

}
