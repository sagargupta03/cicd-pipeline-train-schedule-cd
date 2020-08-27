// Declarative -DSL - Domain specific language //
pipeline
{
	agent any
//	agent 
//	{ label 'master'
//	}
	stages
	{
		stage('Build') 
		{
		steps {
			echo 'Building..'	
			 echo 'Running build automation'
                         sh './gradlew build --no-daemon'
                         archiveArtifacts artifacts: 'dist/trainSchedule.zip'
		      }
		}
		stage('Test')
		{
		steps {
		echo 'Testing..'
		      }
		}
		stage('DeployToStaging')
		{
			when {
                branch 'master'
                           }
                		
                steps {
		echo 'Deploying....'
			  withCredentials([usernamePassword(credentialsId: 'webserver_login_SG', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')])
			  {
				echo 'Credentials step....'  
		         	   sshPublisher(
                                     failOnError : true,
                                    continueOnError : false,
                                    publishers : [
                                       sshPublisherDesc(
                                           configName : 'staging',
                                           sshCredentials : [
                                           username : "$USERNAME",
                                           encryptedPassphrase : "$USERPASS"
                                                             ], 
                                            transfers :    [
                                                sshTransfer(
                                                sourceFiles : 'dist/trainSchedule.zip',
                                                removePrefix : 'dist/',
                                                remoteDirectory : '/tmp',
                                                execCommand : 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule/* && unzip /tmp/trainSchedule.zip -d /opt/train-schedule && sudo /usr/bin/systemctl start train-schedule'
                                                            )
                                                            ]
                                                        )
                                                   ]
                                                 )
				  
			  }
		      }
		}
	}
}
