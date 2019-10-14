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
    stage('Deploy Image') {
      steps{
        script {
        docker.withRegistry('http://10.0.1.113:8081/artifactory', 'jfrog') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
              }
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
}
