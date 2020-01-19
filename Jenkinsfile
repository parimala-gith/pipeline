pipeline {
agent any
stages {
        stage('Build') {
            steps {
                echo 'Building..'
				sh '''
						set +x
						cd c_programs
						echo -e "\n\n**************************** This is a Build JOB **************************** "
						   	make		
							echo -e "\nSTEP 4:	Build Successful"
				  '''
	            }
        }
        stage('deploy') {
            steps {
                echo 'Deploying to TEST environment..'
				sh '''
					
				echo -e "\n\n**************************** This is a Deploy JOB $file **************************** "
				echo "       	ARTIFACTORY_PATH: /home/ec2-user/builds/$file"
				'''
            }
        }
        stage('test') {
            steps {
                echo 'Testing....'
				sh '''
				set +x
					echo -e "\n-------------------------- TEST_CASE ($count) --------------------------"
				   '''
					}
				}
    }
}
