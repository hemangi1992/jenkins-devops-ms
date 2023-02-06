// user name -- admin password-- admin
pipeline{
	agent any
	//agent {docker {image 'maven:3.6.3'}}
	stages {
		stage('Build') {
			steps{
				//sh 'mvn --version'
				echo "$PATH"
				echo "Build number:  $env.BUILD_NUMBER"
				echo "Build id: $env.BUILD_ID"
				echo "$env.JOB_NAME"
				echo "$env.JOB_NAME"
			}
		}

		stage('Test') {
			steps{
				echo "Integration Test"
			}
		}

		stage('Integration Test') {
			steps{
				echo "Integration Test"
			}
		}
	}
	post {
		always {
			echo "I run always."
		}
		success{
			echo "I run only when all stage success."
		}
		failure {
			echo "I run only when any stage fails."
		}
		changed {
			echo "I run only when previous stage and current stage's status mismatch."
		}
	}
}

