pipeline{
    agent any
    environment{
	staging_server=54.196.240.97      
    }
    stages{
	stage('Deploy to Remote)
	    steps{
		sh '''
  		    for fileName in 'find ${WORKSPACE} -type f -mmin -10 |egrep -v ".git | grep -v "Jenkinsfile"'
		    do
      			fil=$(echo ${fileName} | sed 's/'"${JOB_NAME}"'/ /' |awk {'print $2'}0
			'scp -r ${WORKSPACE}${fil} root@$(staging_server):/var/www/html/${fil}
   		    done
  		'''
	    }
    }
}
