node {
  stage 'checkout'
  checkout scm

  stage 'build'
  sh 'touch manifest.json'
  sh 'docker build --tag quay.io/guidesmiths/svc-example:latest .'

  stage 'test'
  
  stage 'publish'
}
