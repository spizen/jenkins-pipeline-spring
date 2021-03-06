machine_nodes = ['c2.exceedcourses.com', 'c1.exceedcourses.com']

pipeline {	
	
    agent any

    stages {
	    
	stage('Cleaning Up previous files') {
            steps {
                echo 'Cleaning up previous files'
		sh '''ssh root@${server} bash -c "'
			rm -rf eco-app
		'"'''
            }
        }
	    
	stage('Cleaning Up previous docker instance') {
            steps {
		
		script {
		  try {
			echo 'Undeploying previous version'
			sh '''ssh root@${server} bash -c "'
				docker stop spring-container
				docker rm spring-container
			'"'''
		  } catch (Exception e) {
		      echo 'Nothing to remove'
		  }
		}    
                
            }
        }
	    
        stage('Cloning Repository') {
            steps {
                echo 'Cloning the repository ...'
		sh '''ssh root@${server} bash -c "'
			mkdir eco-app
			cd eco-app
  			git clone git@gitlab.com:exceed-courses/frontend/eco-spring-frontend.git
		'"'''
            }
        }
        
        stage('Builing the Docker Image') {
            steps {
                echo 'Builing the Docker Image ...'
		    
		sh '''ssh root@${server} bash -c "'
			cd eco-app/eco-spring-frontend/EcoExp/
			docker build -t spring-app -f Dockerfile-Build-Run-Jar .
			docker container run -d --name=spring-container -p 8080:8080 spring-app
		'"'''
		   
            }
        }
	    
	stage('Cleaning Up previous docker instance pre-deployment verification') {
            steps {

		script {
		  try {
			echo 'Undeploying previous version'
			sh '''ssh root@${server} bash -c "'
				docker stop spring-container
				docker rm spring-container
			'"'''
		  } catch (Exception e) {
		      echo 'Nothing to remove'
		  }
		}    
	    
	    }
        }
	    
        stage('Running the Application') {
            steps {
                echo 'Running the application'
		sh '''ssh root@${server} bash -c "'
			docker container run -d --name=spring-container -p 8080:8080 spring-app
		'"'''
            }
        }
    
    }
	
	
}

    @NonCPS
    def echo_all(list) {
        list.each { item ->
            echo "Hello ${item}"
	    sh "ssh root@${item} \"rm -rf eco-app \" "
        }
    }
