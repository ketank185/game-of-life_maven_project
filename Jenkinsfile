pipeline {
	agent {
		label {
			label "built-in"
			customWorkspace "/opt/mayu"
			}
	}
	stages {
		stage ("clean workspace"){
			steps {
			cleanWs()
			}
		}
		stage ("checkout code from git") {
			steps {
			 	checkout scm
			}
		}
		stage ("maven package build") {
			steps {
				sh "mvn clean"
				sh "mvn package"
			}
		}
		stage ("downloading apache tomcat and deploying war in webapps") {
			steps {
				sh 'ansible all -b -m get_url -a "url=https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.73/bin/apache-tomcat-9.0.73.tar.gz dest=/home/mayu" '
				sh 'ansible all -b -m unarchive -a "src=/home/mayu/apache-tomcat-9.0.73.tar.gz dest=/home/mayu/"'
				sh 'ansible all -bm copy -a "src=/opt/mayu/gameoflife-web/gameoflife/gameoflife.war dest=/home/mayu/home/mayu/apache-tomcat-9.0.73/webapps"'
				sh 'ansible all -bm shell -a "src=/home/mayu/apache-tomcat-9.0.73/bin  name=startup.sh"'
				}
		}
	}	
}
