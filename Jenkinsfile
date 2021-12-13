@Library('shared_library_project1') _

pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS=credentials('dockerhub')
  }

  stages {
    stage('show last commit info'){
      steps{
        prepareEnv()
      }
    }

    stage('Build') {
      steps{
        sh 'docker build -t chenint/project1:latest .'
      }
    }
    
    stage('Login') {
      steps{
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'   
      }
    }    
        
    stage('Push') {
      steps{
        sh 'docker push chenint/project1:latest'    
      }
    }
  }
  
  post {
    always {
      sh 'docker logout'
    } 
  }  
}  
