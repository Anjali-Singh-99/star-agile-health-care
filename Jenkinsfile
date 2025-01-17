pipeline {
    agent any

    tools {
        ansible 'Ansible'
        maven 'Maven'
    }

    environment {
        IMAGE_TAG = 'anjalisingh99/health:latest'
        containerName="anjali-heath"
        tag="latest"
        docker_user="anjalisingh99"
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
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'docker_pass', usernameVariable: 'docker_user')]) {
                      sh "docker login -u $docker_user -p $docker_pass"
				      sh "docker tag $containerName:$tag $docker_user/$containerName:$tag"
				      sh "docker push $docker_user/$containerName:$tag"
				      echo "***********image push sucessfully done*********"
            }
                  
                }
                
            }
        }
        stage('deploy')
        {
             steps {
                script {
                    ansiblePlaybook(
                        playbook: 'ansible-playbook.yml',
                        inventory: 'hosts.ini',
                    )
                }
            }
        }
    }
}
