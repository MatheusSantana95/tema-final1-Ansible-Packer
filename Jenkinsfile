pipeline {
    agent any

    environment {
    	ARTIFACTORY_ID = 'Jfrog-Artifactory-Server'
        ARTIFACTORY_URL = credentials('Jfrog-Artifactory-URL')
        ARTIFACTORY_CREDENTIALS = credentials('artifactory-credentials')
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKERHUB_REPOSITORY = credentials('dockerhub-repository')
    }

    stages {
        stage ('Get Artifact') {
            steps {
		rtServer (
		    id: env.ARTIFACTORY_ID,
		    url: env.ARTIFACTORY_URL,
		    username: env.ARTIFACTORY_CREDENTIALS_USR,
		    password: env.ARTIFACTORY_CREDENTIALS_PSW
		)
            
                rtDownload (
		    serverId: env.ARTIFACTORY_ID,
		    spec: '''{
			  "files": [
			    {
			      "pattern": "libs-gradle-dev-local/finalThemeApp/",
			      "target": "finalThemeApp/"
			    }
			  ]
		    }'''
		)
            }
        }
        
        stage ('Docker Build and Deploy') {
            steps {
                sh 'packer build -var "dockerhub_username=$DOCKERHUB_CREDENTIALS_USR" -var "dockerhub_password=$DOCKERHUB_CREDENTIALS_PSW" -var "dockerhub_repository=$DOCKERHUB_REPOSITORY" "templateTemaFinal.json"'
            }
        }
    }
}