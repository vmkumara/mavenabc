pipeline
{
    agent any
    stages
    {
        stage('continuousdownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/maven.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'jenkins is unable to download from remote github', cc: 'git.admin@gmail.com', from: '', replyTo: '', subject: 'download failed', to: ''
                        exit()
                    }    
                }
            }
        }
        stage('continuousbuild')
        {
            steps
            {
                script
                {
                    try
                    {
                          sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                          mail bcc: '', body: 'jenkins is unable to create an artifact from the code', cc: 'dev.team@gmail.com', from: '', replyTo: '', subject: 'build failed', to: ''
                          exit()
                    }
                }
                
            }
        } 
        stage('continuousdeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'scp /var/lib/jenkins/workspace/declarativepipeline1/webapp/target/webapp.war ubuntu@172.31.7.120:/var/lib/tomcat9/webapps/testapp.war'    
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'jenkins is unable to deploy into tomcat on the qaserver', cc: 'middleware.team@gmail.com', from: '', replyTo: '', subject: 'deployment failed', to: ''   
                        exit()
                    }
                }
               
            }
        }
        stage('continuoustesting')
        {
            steps
            {
                script
                {
                    try
                    {
                       git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                       sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline1/testing.jar'    
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'selenium scripts are failed', cc: 'testing.team@gmail.com', from: '', replyTo: '', subject: 'testing failed', to: ''   
                        exit()
                    }
                }
            }
        }
        stage('continuousdelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                       sh 'scp /var/lib/jenkins/workspace/declarativepipeline1/webapp/target/webapp.war ubuntu@172.31.4.16:/var/lib/tomcat9/webapps/prodapp.war'
                    }
                    catch(Exception e5)
                    {
                       mail bcc: '', body: 'jenkins is unable to deploy on tomcat on the prod servers ', cc: 'delivery.team@gmail.com', from: '', replyTo: '', subject: 'delivery failed', to: ''  
                    }
                }
            }
        }
    }
}

