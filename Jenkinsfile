pipeline {
	agent {
		label {
			label "built-in"
		}
	}
	stages {
		stage ("clean workspace") {
			steps {
				cleanWs ()
			}
		}
		stage ("checkout from SCM") {
			steps {
				checkout scm
			}
		}
		stage ("building project") {
			steps {
				sh ''' 
					mvn clean
					mvn package
           '''
			}
		}
		stage ("creating docker conatianers on master") {
			steps {
				sh "sudo docker volume create volume1"
				sh "sudo docker run -itdp 81:8080 -v volume1:/usr/local/tomcat/webapps/ --name tomcatu tomcat"
			}
		}
	}
}
