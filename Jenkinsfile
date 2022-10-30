pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3' } }
	// agent { docker { image 'node:13.8'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh "mvn --version"
				sh "docker version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_ID - $env.BUILD_ID" 
				echo "BUILD_TAG - $env.BUILD_TAG" 
				echo "BUILD_URL - $env.BUILD_URL" 
			}
	    }
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
		        sh "mvn test"
			}
	    }
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
	    }
		
	} 
	post {
		always {
			echo 'i run  always'
		}
		success {
			echo 'i run when you are successful'
		}
		failure {
			echo 'i run when you fail'
		}
	}
}
