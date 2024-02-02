pipeline {
    agent any
    stages {
        stage('Build Maven') {
            steps {
                sh 'pwd'
                sh 'mvn clean install package'
            }
        }
        stage('copy artifacts') {
            steps {
                sh 'pwd'
                sh 'cp -r target/*.jar docker'
            }
        }
        stage ('unit tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage('build docker image'){
            steps {
                script {
                    def customImage = docker.build("kamleshamrute/petclinic:${env.BUILD_NUMBER}", "./docker")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    customImage.push() 
                }
            }
        }
    }
}
 