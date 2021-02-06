pipeline {
	agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
      stage('Build')
	  {
		steps {
		  sh 'mvn --version'
		  echo "Build"
		  echo "PATH - $PATH"
		  echo "BUILD_NUMBER - $env.BUILD_NUMBER"
		  echo "BUILD_ID - $env.BUILD_ID"
		  echo "BUILD_TAG - $env.BUILD_TAG"
		  echo "BUILD_URL - $env.BUILD_URL"
		  echo "JOB_NAME - $env.JOB_NAME"

		}
	  }
	  stage('Test') 
	  {
		steps {
		  echo "Test"
	    }
	  }
	  stage('Integration Test') 
	  {
		steps {
		  echo " Test"
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
