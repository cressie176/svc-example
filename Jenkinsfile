node {
  stage 'build'
  sh 'docker-compose -f docker/docker-compose-build.yml build'

  stage 'test'
  
  stage 'publish'
}
