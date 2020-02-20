def tomcat = "13.58.116.132"
pipeline{
	agent { label 'Ajenkins-slave1' }
	stages{
		stage('checkout'){
			steps{
				checkout([$class: 'GitSCM', 
    branches: [[name: '*/devchild']], 
    userRemoteConfigs: [[credentialsId: 'f176d7a8-8993-4be5-81eb-267deaa3a23f	', url: 'https://github.com/vinaydigumarthi/mavenrepo.git']]
])

			     }
					   }
		stage('build'){
			steps{
				
				sh "mvn package"
			
				 }
                    }
		stage('sonar-jenkins'){
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
