pipeline
{
    agent any
    stages
    {
        stage('continuousdownload_loans')
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
        stage('continuousbuild_loans')
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
 
