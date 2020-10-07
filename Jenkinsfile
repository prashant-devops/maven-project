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
   }
}
