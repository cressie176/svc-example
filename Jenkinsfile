node {
  stage 'env'
  sh 'env'

  stage 'build'
  sh 'docker-compose -f docker/docker-compose-build.yml build'

  stage 'test'
  try {
    sh 'docker-compose -f docker/docker-compose-yml run --rm -e SERVICE_ENV=build svc-example node_modules/.bin/mocha tests'
  } finally {
    docker-compose -f docker/docker-compose-build.yml stop
  }
  
  stage 'publish'
}
