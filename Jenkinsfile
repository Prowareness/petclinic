#!groovy
stage('Commit') {
  node {
    checkout scm
    
    def image = docker.build('harmpauw/petclinic')
    docker.withRegistry('https://index.docker.io/v1/','b7dafb21-aace-43b3-b765-f63a508085b2') {
      image.push('test')
    }
  }
}

stage('Test') {
  node {
    checkout scm
    
    sh "sed 's#:latest#:test#' kubernetes/deployments/app.yaml | kubectl apply -f -"
    
  }
}
