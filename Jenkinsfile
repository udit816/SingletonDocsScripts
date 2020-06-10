node {
	stage('Code Checkout') {
		git 'http://172.16.1.252:8084/root/hpgreenfield-partner.git'
	}

	stage('Compile and Package') {
		env.JAVA_HOME="${tool 'java8'}"
		env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
		env.MAVEN_HOME="${tool 'maven36'}"
		sh 'mvn clean package'
	}
	
	stage('SonarQube Analysis') {
        withSonarQubeEnv('sonarqube') { 
          sh 'mvn sonar:sonar'
        }
    }


/*	stage('Deploy to Tomcat') {
		sshagent(['tomcat-deployer']) {
			sh 'scp -o StrictHostKeyChecking=no target/*.war udit816@localhost:/opt/apache-tomcat/webapps/'
		}
	}*/
}
