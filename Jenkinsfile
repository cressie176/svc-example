node {
  stage 'checkout'
  checkout scm

  stage 'build'
  sh 'touch manifest.json'
  sh 'docker build --tag quay.io/guidesmiths/svc-example:latest .'

  stage 'test'
  try {
    sh 'docker-compose -f docker/docker-compose-test.yml'
  } finally {
    sh 'docker-compose -f down'
  }
  
  stage 'publish'
}
