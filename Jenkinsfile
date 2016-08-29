node {
  stage 'checkout'
  checkout scm
  println env.GIT_COMMIT
  
  stage 'build'
  sh 'docker-compose -f docker/docker-compose-build.yml build'

  stage 'test'
  
  stage 'publish'
}
