node {
  stage 'checkout'
  checkout scm
  
  stage 'build'
  sh "echo ${env.GIT_COMMIT}"
  sh 'ls -1'
  // sh 'docker-compose -f docker/docker-compose-build.yml build'

  stage 'test'
  
  stage 'publish'
}
