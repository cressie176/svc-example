node {
  stage 'checkout'
  checkout scm

  stage 'manifest'
  sh 'echo {} > manifest.json'

  stage 'build'
  sh 'docker-compose -f docker/docker-compose-build.yml build svc-example'

  stage 'test'
  try {
    sh 'docker-compose -f docker/docker-compose-build.yml run --rm -e SERVICE_ENV=build svc-example bash -c \'sleep 5 && node_modules/.bin/mocha tests\''
  } finally {
    sh 'docker-compose -f docker/docker-compose-build.yml down'
  }
  
  stage 'publish'
}
