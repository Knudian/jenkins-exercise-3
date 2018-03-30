pipeline {
	agent any

	stages {
		stage('setup') {
		    withCredentials(bindings: [
                string(credentialsId: paramUsername, variable: 'username'),
                string(credentialsId: paramDatabase, variable: 'database'),
                string(credentialsId: paramPassword, variable: 'password')
            ]) {
                // Reading configuration file
                String configFile =
                def config =
                // Writing credentials
                config.user = username
                config.database = database
                config.password = password
                def json = groovy.json.JsonOutput.toJson(config)
                // Write new file
                writeFile file: "conf/bdd.conf", text: json
            }
		}
	    stage('archive') {
	        steps {
	            archiveArtifacts 'conf/*'
	        }
	    }
	}
}