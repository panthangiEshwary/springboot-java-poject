pipeline {   
    agent any 
    tools{
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/panthangiEshwary/springboot-java-poject.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        
        stage('Package') {
            steps {
                sh "mvn clean package"
            }
        }

        stage('Deploy') {
            steps {
                sh "scp target/spring-boot-web.jar user@54.226.17.124:/home/user/app/"
            }
        }

        stage('Restart App') {
            steps {
                sh """
                ssh user@54.226.17.124 '
                mkdir -p /home/user/app/logs
                pkill -f spring-boot-web.jar || true
                nohup java -jar /home/user/app/spring-boot-web.jar > /home/user/app/logs/logs.txt 2>&1 &
                '
                """
            }
        }
    }
}

