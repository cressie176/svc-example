node {
  stage 'build'
  sh 'docker-compose -f docker/docker-compose-build.yaml build'

  stage 'test'
  
  stage 'publish'
}
