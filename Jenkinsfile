pipeline {
  agent any
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t dockersamples/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t dockersamples/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t dockersamples/worker ./worker'
      }
    }
    stage('Push result image') {
           {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jfrog', url:'http://10.0.1.113:8081/artifactory') {
          sh 'docker push dockersamples/result'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jfrog', url:'http://10.0.1.113:8081/artifactory') {
          sh 'docker push dockersamples/vote'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jfrog', url:'http://10.0.1.113:8081/artifactory') {
          sh 'docker push dockersamples/worker'
        }
      }
    }
  }
}
