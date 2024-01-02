pipeline{
  agent any

  tools{
    ansible 'Ansible'
    maven 'Maven'
  }
  environment{
    IMAGE_TAG = 'anjalisingh99/health:latest'
  }
  stages{
    stage('checkout'){
      steps{
        git 'https://github.com/Anjali-Singh-99/star-agile-health-care.git'
      }
    }
  }
}
