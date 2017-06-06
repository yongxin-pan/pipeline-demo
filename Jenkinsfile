#!/usr/bin/env groovy

pipeline {
	agent any
	
	stages {
		stage('Build') {
			steps {
				echo 'Building..'
			}
		}
		stage('Version Handling') {
			steps {
				def version = null
				if (binding.variables.get() == 'release') {
					version = "${MAJOR}.${MINOR}.${PATCH}.${env.BUILD_NUMBER}"
				} else {
					branch = ("branch-${env.BUILD_NUMBER}-${env.BRANCH_NAME}" =~ /\\|\/|:|"|<|>|\||\?|\*|\-/).replaceAll("_")
					version = "0.0.0-${branch}.${env.BUILD_NUMBER}"
				}
		
				//output the version info to a file version.txt
				writeFile([file: 'version.txt', text: version])}
				archive('version.txt')
		}		
		stage('Deploy') {
			steps {
				echo 'Deploy..'
			}
		}
	}
	
}
