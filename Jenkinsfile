pipeline
{

   agent any
   stages
   {
        stage ('SCM Checkout')
        {
            steps
            {
               git branch: 'master', url: 'https://github.com/prashant-devops/maven-project'
            }
        }
        stage ('Compile SRC')
        {
            steps
            {
               withMaven(jdk: 'local-jdk-11', maven: 'local-maven-3.6'') 
               {
                  sh 'mvn compile'
               }
            }  
        }
		stage ('Test')
		{
            steps
            {
               withMaven(jdk: 'local-jdk-11', maven: 'local-maven-3.6'') 
               {
                  sh 'mvn test'
               }
            }  
        }
		stage ('Build my job')
		{
            steps
            {
               withMaven(jdk: 'local-jdk-11', maven: 'local-maven-3.6'') 
               {
                  sh 'mvn package'
               }
            }  
        }
		stage ('TomCat deployment')
		{
            steps
            {
               sshagent(['deploy-tomcat']) 
				{
					sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@13.127.9.171:/var/lib/tomcat/webapps'
				}
            }  
        }
   }
}
