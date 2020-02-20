def tomcat = "3.16.159.111"
pipeline{
	agent { label 'dev' }
	stages{
		stage('checkout'){
			steps{
				checkout([$class: 'GitSCM', 
    branches: [[name: '*/newfunctionality']], 
    userRemoteConfigs: [[credentialsId: '7b07438b-9285-40ff-991b-8b9449f1f818', url: 'https://github.com/projectgit123/mavenrepo.git']]
])

			     }
					   }
		stage('build'){
			steps{
				sh "mvn package"
			
				 }
                    }
		stage('sonar'){
			steps{
				withSonarQubeEnv('sonar'){
				sh "mvn sonar:sonar"
				}
			      }
					   }
		stage('deploy'){
			steps{
			sh "ssh $tomcat systemctl stop tomcat"
			sh "scp target/*.war $tomcat:/var/lib/tomcat/webapps"	
			sh "ssh $tomcat systemctl start tomcat"
			}
		}
		  }
		}
