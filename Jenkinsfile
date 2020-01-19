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
					file="$(pwd)/c_programs/ABC.exe"
					[[ -f "$file" ]] && sudo rm -f "$file"
					pwd; sudo chmod 777 build; ./build 1> /dev/null
					
				echo -e "\n\n**************************** This is a Deploy JOB for $file**************************** "
				if [[ -f "$file" ]]; then 
				count=1
				
				for i in {1..10}
				do
					oe=$((1000 + RANDOM % 10000))
					fact=$((1 + RANDOM % 15))
					num1=$((1 + RANDOM % 100))
					num2=$((1 + RANDOM % 1000))
					
						echo -e "\n-------------------------- TEST_CASE ($count) --------------------------"
						$file -v -i <<<"$fact $oe $num1 $num2"
					
					if [ $? -eq 0 ]; then
						echo -e "\n      RESULT -> TEST_CASE (${count}): SUCCESS" 
					else  
						echo -e "\n      RESULT -> TEST_CASE (${count}): FAILED"
						exit 1
					fi

					echo "-------------------------------------------------------------------"
					((count++))
				done
				else 
					 echo -e "**************** ERROR *********************\n"
					  echo "Build - ABC.exe notfound $file "
					  echo -e "********************************************\n"
					  exit 1
				fi
				'''
					}
				}
    }
}
