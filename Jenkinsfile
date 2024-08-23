pipeline {
    agent any

//	tools {
//		jdk 'jdk8'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "Atiksh@9980" scp target/gamutkart.war atiksh@172.17.0.2:/home/atiksh/Devops/apache-tomcat-9.0.93/webapps'
                sh 'sshpass -p "Atiksh@9980" ssh atiksh@172.17.0.2 "/home/atiksh/Devops/apache-tomcat-9.0.93/bin/startup.sh"'
            }
        }
    }
}
