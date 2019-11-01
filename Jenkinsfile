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
	    
	stage ('Sonar Analysis Stage') {
            steps {
                withMaven(maven : 'apache-maven-3.6.0') {
                    bat 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000/sonar'
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
					
				//jacoco classPattern: '**/target/classes', exclusionPattern: '**/*Test*.class', execPattern: '**/target/coverage-results/**.exec', inclusionPattern: '**/*.class'
			
				//jacoco( execPattern: 'target/*.exec', classPattern: 'target/classes', sourcePattern: 'src/main/java', exclusionPattern: 'src/test*')
			
				//jacoco buildOverBuild: true, changeBuildStatus: true, deltaBranchCoverage: '80', deltaClassCoverage: '70', deltaComplexityCoverage: '70', deltaInstructionCoverage: '80', deltaLineCoverage: '70', deltaMethodCoverage: '70', maximumBranchCoverage: '80', maximumClassCoverage: '70', maximumComplexityCoverage: '70', maximumInstructionCoverage: '80', maximumLineCoverage: '70', maximumMethodCoverage: '70', minimumBranchCoverage: '20'	
				//jacoco()
				jacoco maximumBranchCoverage: '10', maximumClassCoverage: '10', maximumComplexityCoverage: '10', maximumInstructionCoverage: '10', maximumLineCoverage: '10', maximumMethodCoverage: '10'
				//influxDbPublisher customPrefix: '', customProjectName: 'Jenkins Pipeline Statistics', jenkinsEnvParameterField: '''Jenkins=CI''', jenkinsEnvParameterTag: 'git=scm',selectedTarget: 'jenkins'
				
				//influxDbPublisher customPrefix: '',selectedTarget: 'jacoco'
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
