// Declarative -DSL - Domain specific language //
pipeline
{
	agent any
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
		stage('Deploy')
		{
                		
                steps {
		echo 'Deploying....'
		      }
		}
	}
}
