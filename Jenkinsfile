pipeline {

    agent any

   

    stages {
		
		stage ('Checkout') {
			Steps {

           			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'c0587111-ea11-43a8-8c41-5a54b4e6b80b', url: 'https://github.com/ravigrv21290/SpringBootJenkinsPOC.git']]])

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

}
