pipeline {
	agent {
		label {
			label "built-in"
			
			}
		}
		tools {
		jdk "java-8"
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
				sh 'ansible all -b -m unarchive -a "src=/home/mayu/apache-tomcat-9.0.73.tar.gz dest=/home/mayu/ remote_src=yes"'
				sh 'ansible all -bm copy -a "src=/var/lib/jenkins/workspace/ansible-2/gameoflife-web/target/gameoflife.war dest=/home/mayu/apache-tomcat-9.0.73/webapps"'
				sh 'ansible all -bm script -a "name:/home/mayu/apache-tomcat-9.0.73/bin/startup.sh remote_src=yes"'
				}
		}
	}	
}
