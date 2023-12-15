pipeline{
    agent any
    environment {
     DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  	}
    stages {

        stage('Getting project from CDCI-Checkpoint') {
            steps{
      			checkout([$class: 'GitSCM', branches: [[name: '*/main']],
			extensions: [],
			userRemoteConfigs: [[url: 'https://github.com/Omar-Bensalah/first-lab-project.git']]])
            }
        }

       stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t omarbensalah8/firstlabphase .'
      }
    }
       //stage('Docker login') {
       // agent any
        // steps {
          //withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        //	sh 'docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}'
         // }
       //}
stage('Login to docker hub') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
     }

      stage ('Docker push to hub') {
        agent any
        steps {
          sh 'docker push omarbensalah8/firstlabphase:latest'
        }
      }
}
	    
        post {
        success {
            echo "Succesfull pipeline"
        }
  
    }	
}
       

