// user name -- admin password-- admin
pipeline{
	agent any
	//agent {docker {image 'maven:3.6.3'}}

	environment {
		dockerHome = tool "myDocker"
		mavenHome = tool "myMaven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "$PATH"
				echo "Build number:  $env.BUILD_NUMBER"
				echo "Build id: $env.BUILD_ID"
				echo "$env.JOB_NAME"
				echo "$env.JOB_NAME"
			}
		}

		stage('Compile'){
			steps{
				sh 'mvn clean compile'
			}
		}

		stage('Test') {
			steps{
				sh 'mvn test'
			}
		}

		stage('Integration Test') {
			steps{
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}

		stage('Package') {
			steps{
				sh 'mvn package -DskipTests'
			}
		}

		stage('Build Docker Image'){
			steps{
				// 'docker build -t renish1311/currency-exchange-devops:$env.BUILD_TAG'
				script{
					dockerImage = docker.build("renish1311/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps{
				script{
					docker.withRegistry('','dockerhub'){
							dockerImage.push()
							dockerImage.push('latest')
					}
					
				}
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

