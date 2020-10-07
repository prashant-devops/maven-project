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
               withMaven(jdk: 'local-jdk', maven: 'local-maven') 
               {
                  sh 'mvn compile'
               }
            }  
        }
		stage ('Test')
		{
            steps
            {
               withMaven(jdk: 'local-jdk', maven: 'local-maven') 
               {
                  sh 'mvn test'
               }
            }  
        }
		stage ('Build my job')
		{
            steps
            {
               withMaven(jdk: 'local-jdk', maven: 'local-maven') 
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
					sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@13.235.132.119:/var/lib/tomcat/webapps'
				}
            }  
        }
   }
}
