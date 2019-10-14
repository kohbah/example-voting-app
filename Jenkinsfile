node {
    def resultImage
    def voteImage
    def workerImage
    docker.withRegistry("http://10.0.1.113:8081/artifactory", "jfrog" ) { 
      stage('Clone repo') {
        checkout scm
      }
      stage('Build result') {
        resultImage = docker.build("dockersamples/result", "./result")
      } 
      stage('Build vote') {
        voteImage = docker.build("dockersamples/vote", "./vote")
      }
      stage('Build worker dotnet') {
        workerImage = docker.build("dockersamples/worker", "./worker")
      }
      stage('Push result image') {
          resultImage.push("${env.BUILD_NUMBER}")
          resultImage.push()
      }
      stage('Push vote image') {
          voteImage.push("${env.BUILD_NUMBER}")
          voteImage.push()
      }
      stage('Push worker image') {
          workerImage.push("${env.BUILD_NUMBER}")
          workerImage.push()
      }
    }
}
