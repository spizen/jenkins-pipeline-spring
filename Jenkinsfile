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
                sh '''
                ssh root@c2.exceedcourses.com >> ENDSSH
				touch b_file
				mkdir eco-app
				cd eco-app
				touch c_file
                ENDSSH
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    
    }
}
