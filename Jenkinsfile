pipeline {
	
    environment {
	machine_nodes = ['c2.exceedcourses.com', 'c1.exceedcourses.com']
   }	
	
    agent any

    stages {
        
	stage('Touch') {
            steps {
                echo 'Touch'
		script {
                    for (int i = 0; i < machine_nodes.size(); ++i) {
                        sh '''ssh root@${machine_nodes[i]} bash -c "'
			touch A
			'"'''
                    }
                }
		
            }
        }    
	    
	stage('Cleaning Up previous files') {
            steps {
                echo 'Cleaning up previous files'
		sh '''ssh root@c2.exceedcourses.com bash -c "'
			rm -rf eco-app
		'"'''
            }
        }
	    
	stage('Cleaning Up previous docker instance') {
            steps {
                echo 'Undeploying previous version'
		sh '''ssh root@c2.exceedcourses.com bash -c "'
			docker stop spring-container
			docker rm spring-container
		'"'''
            }
        }
	    
        stage('Cloning Repository') {
            steps {
                echo 'Cloning the repository ...'
		sh '''ssh root@c2.exceedcourses.com bash -c "'
			mkdir eco-app
			cd eco-app
  			git clone git@gitlab.com:exceed-courses/frontend/eco-spring-frontend.git
		'"'''
            }
        }
        
        stage('Builing the Docker Image') {
            steps {
                echo 'Builing the Docker Image ...'
		    
		sh '''ssh root@c2.exceedcourses.com bash -c "'
			cd eco-app/eco-spring-frontend/EcoExp/
			docker build -t spring-app -f Dockerfile-Build-Run-Jar .
			docker container run -d --name=spring-container -p 8080:8080 spring-app
		'"'''
		   
            }
        }
	    
	stage('Cleaning Up previous docker instance pre-deployment verification') {
            steps {
                echo 'Undeploying previous version'
		sh '''ssh root@c2.exceedcourses.com bash -c "'
			docker stop spring-container
			docker rm spring-container
		'"'''
            }
        }
	    
        stage('Running the Application') {
            steps {
                echo 'Running the application'
		sh '''ssh root@c2.exceedcourses.com bash -c "'
			docker container run -d --name=spring-container -p 8080:8080 spring-app
		'"'''
            }
        }
    
    }
}
