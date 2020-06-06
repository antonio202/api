pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
			bat 'whoami'
			bat 'vagrant up'
			}
		}
		stage('Test') {
			steps {
				echo 'TEST'
				bat 'vagrant halt'
				bat 'vagrant package --base API-Vagrant'
			}
		}
		stage('Push registry') {
			steps {
				withCredentials([string(credentialsId: 'token', variable: 'token')]) {
				bat 'vagrant cloud auth login -t $token'
				bat 'vagrant cloud publish antjos/api 1 antjos package.box -f'
				}
			}
		}
		stage('Initiate') {
			steps {
				bat 'vagrant up'
				bat 'vagrant provision'
			}	
		}
	}
}
