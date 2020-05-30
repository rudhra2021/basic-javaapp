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
  
        stage('SonarQube analysis') {
    def mvnHome = tool name: 'maven3', type: 'maven'
    withSonarQubeEnv('sonar') { // If you have configured more than one global server connection, you can specify its name
      sh "${mvnHome}/bin/mvn sonar:sonar"
    }
  }
        
        stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
                mail bcc: '', body: '''hi,
                jenkins qg.status
                ''', cc: '', from: '', replyTo: '', subject: 'jenkins-alert-mail', to: 'sasidharallnew@gmail.com'
                  
               if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
                  mail bcc: '', body: '''hi,
                  jenkins qg.status
                  ''', cc: '', from: '', replyTo: '', subject: 'jenkins-alert-mail', to: 'sasidharallnew@gmail.com'
      
              }
          }
        }
        
        stage("email notification")
        {
                mail bcc: '', body: '''hi,
jenkins mail alert
''', cc: '', from: '', replyTo: '', subject: 'jenkins-alert-mail', to: 'sasidharallnew@gmail.com'
        }
}
