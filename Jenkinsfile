pipeline {
    agent any
    stages {
        stage('Clone the repo') {
            steps {
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Build Image') {
            steps {
                sh 'cp target/addressbook.war .'
                sh 'docker build -t myimagejenkins .'
            }
        }
        stage('Push image to dockerhub') {
            steps {
                sh 'docker tag myimagejenkins edu123/myimagejenkins:$BUILD_NUMBER'
                sh 'docker login --username edu123 --password Edureka@123'
                sh 'docker push edu123/myimagejenkins:$BUILD_NUMBER'
            }
        }
        stage('Create Containers') {
            steps {
                sh 'docker run -d -p 8080:80 myimagejenkins'
            }
        }
    }
}
