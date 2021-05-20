def container_name = "my_app_cont"
def image_name = "my_app_img"
def container_found = ""

pipeline {
    agent any

    stages {
        stage('clone git') {
            steps {
                git 'https://github.com/AyaAymanMohamed/NGINX-Demos.git'
            }
        }
        stage('clear') {
            steps {
                script {
                    container_found = sh (script: "docker ps -a -f name=${container_name}", returnStdout: true).trim()
                    if(!container_found.isEmpty()){
                        sh "docker container stop ${container_name}"
                        sh "docker container rm ${container_name}"
                    }
                }
                    
                }
            }
        stage('build image') {
            steps {
                sh "docker build -t ${image_name} https://github.com/AyaAymanMohamed/NGINX-Demos.git#master:nginx-hello"
                sh "docker run --name ${container_name} -dp 3030:80 ${image_name}"
                sh 'docker container ps'
            }
            
        }
    }
}

