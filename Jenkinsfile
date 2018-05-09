pipeline{
    agent any
    environment {
        imageName = "champ6803/hello-nginx"
    }
    stages {
        stage("Prepare"){
            steps {
                echo "Hello World"
            }
        }
        stage("check version"){
            steps {
                sh "docker --version"
            }
        }
        stage("build image"){
            steps {
                sh "docker build -t ${env.imageName}:1.${env.BUILD_NUMBER} ."
                sh "docker tag ${env.imageName}:1.${env.BUILD_NUMBER} hello-nginx"
            }
        }
        stage("push image") {
            steps {
                script {
                    docker.withRegistry(
                        'https://registry.hub.docker.com', 'docker-id'
                    ) {
                        def image = docker.build("${env.imageName}:1.${env.BUILD_NUMBER}")
                        image.push()
                    }
                }
            }
        }
    }
}