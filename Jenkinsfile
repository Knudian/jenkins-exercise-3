pipeline {
	agent any

	environment {
	    username = credentials(paramUsername)
	    database = credentials(paramDatabase)
	    password = credentials(paramPassword)
	}

	String configFile = ''
	def config = null
	def json = null

	stages {
		stage('setup') {
		    steps {
		        configFile = readFile "conf/bdd.conf"
		    }
		    steps {
		        config =  new groovy.json.JsonSlurperClassic().parseText(configFile)
		    }
		    steps {
		        config.user = username
		        config.database = database
		        config.password = password
		    }
		    steps {
		        json = groovy.json.JsonOutput.toJson(config)
		    }
		    steps {
                writeFile file: "conf/bdd.conf", text: json
		    }
		    steps {
		        archiveArtifacts 'conf/*'
		    }
		}
	}
}