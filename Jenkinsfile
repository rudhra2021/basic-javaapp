node
{
stage("git-pull")
        {       
        git 'https://github.com/rudhra2021/basic-javaapp.git'
        }

stage("compile-package")
        {
def mvnHome = tool name: 'maven3', type: 'maven'
sh "${mvnHome}/bin/mvn package"
        }
        stage("email notification")
        {
                mail bcc: '', body: 'Find the attached jenkins ststus.', cc: '', from: '', replyTo: '', subject: 'Jenkinspipeline', to: 'sasidharallnew'
        }
}

