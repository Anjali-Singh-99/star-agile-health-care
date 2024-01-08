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
                    def dockerUsername = 'anjalisingh99'
                    def dockerPassword = 'Anjali@123'
                    
                    sh "echo '${dockerPassword}' | docker login -u '${dockerUsername}' --password-stdin"
                    def customImage = docker.build(IMAGE_TAG)
                    customImage.push()
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
