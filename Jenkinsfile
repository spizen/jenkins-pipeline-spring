pipeline {
    agent any

    stages {
        
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'ssh root@c2.exceedcourses.com "touch a_file" '
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing..'
		    
		sh '''ssh root@c2.exceedcourses.com bash -c "'
  			cd Desktop/testfolder
  			java -cp xyz.jar Main
		'"'''
		   
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    
    }
}
