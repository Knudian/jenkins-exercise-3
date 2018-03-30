pipeline {
	agent any 

	stages {
		stage('setup') {
			steps {
			    node {
                    withCredentials([
                        string(credentialsId: paramUsername, variable: 'username'),
                        string(credentialsId: paramDatabase, variable: 'database'),
                        string(credentialsId: paramPassword, variable: 'password')
                    ]) {
                        // Reading configuration file
                        String configFile = readFile "conf/bdd.conf"
                        def config = new groovy.json.JsonSlurperClassic().parseText(configFile)
                        // Writing credentials
                        config.user = username
                        config.database = database
                        config.password = password
                        def json = groovy.json.JsonOutput.toJson(config)
                        // Write new file
                        writeFile file: "conf/bdd.conf", text: json
                    }
                }
			}
		}
	    stage('archive') {
	        steps {
	            archiveArtifacts 'conf/*'
	        }
	    }
	}
}