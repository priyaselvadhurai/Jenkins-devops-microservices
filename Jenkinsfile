pipeline {
	agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
      stage('Checkout')
	  {
		steps {
		  sh 'mvn --version'
		  sh 'docker version'
		  echo "Build"
		  echo "PATH - $PATH"
		  echo "BUILD_NUMBER - $env.BUILD_NUMBER"
		  echo "BUILD_ID - $env.BUILD_ID"
		  echo "BUILD_TAG - $env.BUILD_TAG"
		  echo "BUILD_URL - $env.BUILD_URL"
		  echo "JOB_NAME - $env.JOB_NAME"

		}
	  }
	   stage('Compile'){
         steps{
            sh "mvn clean compile"
		  }
	  }
	   stage('Test') 
	  {
		 steps {
		   sh "mvn test"
	    }
	  }
	   stage('Integration Test') 
	  {
		 steps {
		   sh "mvn failsafe:integration-test failsafe:verify"
		}
	  }
	   stage('Package') 
	  {
		 steps {
		   sh "mvn package -DskipTests"
		}
	  }
	   stage('Build Docker Image')
	  {
		 steps{
          //"docker build -t lakshmisharp/currency-exchange-devops:$env.BUILD_TAG"
           script{
             dockerImage = docker.build("lakshmisharp/currency-exchange-devops:${env.BUILD_TAG}")
		      }
		  }
	  }
	   stage('Push Docker Image')
	  {
		 steps{
		   script{
			 docker.withRegistry('https://registry.hub.docker.com','dockerhub'){
			   dockerImage.push("${env.BUILD_NUMBER}");
			   dockerImage.push("latest");
			  }
			}
		  }
	  }
    } 
	post {
		always{
			echo ' Im awesome, I run always'
		}
		success{
			echo "I run when you are success"
		}
		failure{
			echo "I run when you fail"
		}
	}
 }
