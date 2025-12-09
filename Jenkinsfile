pipeline { 
    agent any 
    stages { 
        stage('Build with Maven') { 
            steps { 
                sh 'mvn clean package' 
            } 
        } 
        stage('Build Docker Image') { 
            steps { 
                script { 
                    docker.build("demo-maven-image") 
                } 
            } 
        } 
    } 
} 
