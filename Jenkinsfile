pipeline {
    agent any

    tools {
        ansible 'Ansible'
        maven 'Maven'
    }

    environment {
        IMAGE_TAG = 'anjalisingh99/health:latest'
    }

    stages {
        stage('checkout') {
            steps {
                git 'https://github.com/Anjali-Singh-99/star-agile-health-care.git'
            }
        }

        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('docker build and push') {
            steps {
                script {
                    def (containerName, tag) = IMAGE_TAG.tokenize(':')

                    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'docker_pass', usernameVariable: 'docker_user')]) {
                        // Docker login
                        sh "docker login -u $docker_user -p $docker_pass"
                        
                        // Docker build
                        sh "docker build -t $containerName:$tag ."

                        // Docker tag
                        sh "docker tag $containerName:$tag $docker_user/$containerName:$tag"

                        // Docker push
                        sh "docker push $docker_user/$containerName:$tag"

                        echo "*********** Image push successfully done *********"
                    }
                }
            }
        }
    }
}
