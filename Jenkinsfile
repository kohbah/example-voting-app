pipeline {
  agent any
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t dockersamples/result:latest ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t dockersamples/vote:latest ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t dockersamples/worker:latest ./worker'
      }
    }
    stage('Push result image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jfrog', url:'http://10.0.1.113:8081/artifactory') {
          sh 'docker push dockersamples/result:latest'
        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jfrog', url:'http://10.0.1.113:8081/artifactory') {
          sh 'docker push dockersamples/vote:latest'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'jfrog', url:'http://10.0.1.113:8081/artifactory') {
          sh 'docker push dockersamples/worker:latest'
        }
      }
    }
  }
}
