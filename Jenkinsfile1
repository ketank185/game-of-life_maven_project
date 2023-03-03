pipeline {
	agent {
		label {
			label "slave-1"
		}
	}
	stages {
		stage("clean workspace") {
            steps{
                //sh "sudo rm -rf /opt/jenkins-slave/workspace/assignment1(22.02.23)/*"
		    cleanWs ()
            }
            
        }
		stage ("build maven project") {
			steps {
			    // sh "rm -rf /opt/jenkins-slave/workspace/assignment1(22.02.23)"
			    // sh "export PATH=$PATH:/opt/apache-maven-3.9.0/bin"
			    //sh "sudo git clone https://github.com/ketank185/game-of-life_maven_project.git" 
			    sh "sudo cd /opt/jenkins-slave/workspace/assignment1(22.02.23)/game-of-life sudo mvn clean package"
		}
		}
			}
}
