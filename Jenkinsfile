pipeline {
    agent any
    tools {
	maven 'maven'
}

    parameters {

        choice(name: 'CHOICE', choices: ['1.1', '1.2', '1.3'], description: 'Pick a version')

}
        
	stages {
	    
        stage('build jar') {
            steps {
		  
                  echo "building application version ${params.CHOICE}"
		  sh 'mvn clean package'
		    
         }                        
      }
   
    	stage('build image') {
            steps {
		     
                    echo "building docker image"
		    withCredentials([usernamePassword(credentialsId: 'docker-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
			  
		    sh "docker build -t usama07/demo-app:${params.CHOICE} ."
		    sh "docker login -u $USER -p $PASS"
		    sh "docker push usama07/demo-app:${params.CHOICE}"
		                     
            }
        }
   }

	    

        stage('deploy') {
            steps {
		    
                    echo "deploying the application version ${params.CHOICE}"
                    
            
         }   
       }
     }
}
