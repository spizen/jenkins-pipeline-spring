pipeline {
    agent any

    stages {
        
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'echo "Today is:" date'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    
    }
}
