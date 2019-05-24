pipeline {
	
	agent any 

    stages {		
	stage ('Checkout') {
		steps {
			git 'https://github.com/ravigrv21290/SpringBootJenkinsPOC.git'
		}          
        }
		
        stage ('Compile Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.6.0') {
                    bat 'mvn clean install'               
                }
            }
        }

        stage ('Testing Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.6.0') {
                    bat 'mvn test'
                }
            }
        }
		
        stage ('Package Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.6.0') {
                    bat 'mvn package'
                }
            }
        }
    }

	post {
        	always {
            		echo 'Copying artifacts'
					
					//archiveArtifacts 'target/surefire-reports/*.xml'
					
					// It takes all files from source like .java,.class,.jar,xml etc
					// archive '**'  
					
					// takes all .xml files
					// archive '**/*.xml'
					
					archive 'target*//*.jar'
					// copy only target files
	
					//copyArtifacts filter: 'target*//*.jar', fingerprintArtifacts: true, projectName: 'Multibranch-Pipeline/master', target: '/var/lib/jenkins/ravi'
	
					//copyArtifacts filter: 'target/surefire-reports/*.xml', fingerprintArtifacts: true, flatten: true, projectName: 'Multibranch-Pipeline/master', target: '/var/lib/jenkins/ravi'	

					//copyArtifacts filter: '', fingerprintArtifacts: true, flatten: true, projectName: 'Multibranch-Pipeline/master', target: '/var/lib/jenkins/ravi'	
			}

        	success {
            		echo 'I succeeeded!'
        	}

        	unstable {
            		echo 'I am unstable :/'
        	}

        	failure {
            		echo 'I failed :('
        	}
	}
}
