pipeline {
    agent any
    
    stages {
        stage(clone) {
            steps {
                git 'https://github.com/ravinaj21/Amazon.git'
            }
        }
        stage(build) {
            steps {
                sh 'mvn -f Amazon/pom.xml clean install -DskipTests'
            }
        }
        stage(test) {
            steps {
                sh 'mvn -f Amazon/pom.xml test'
            }
            post {
				always {
					archiveArtifacts 'Amazon/Amazon-Web/target/*.war'
					
					junit 'Amazon/Amazon-Core/target/surefire-reports/*.xml'
				}
			}
        }
        stage(deploy) {
            steps {
                sh './Amazon/scripts/deploy.sh'
            }
        }
        stage(start) {
            steps {
                sh './Amazon/scripts/start.sh'
            }
        }
    }
}   
