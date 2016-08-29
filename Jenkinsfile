node {
  stage 'checkout'
  checkout scm

  stage 'build'
  sh 'touch manifest.json'
  sh 'docker build --tag quay.io/guidesmiths/svc-example:latest .'

  stage 'test'
  try {
    sh 'docker-compose -f docker/docker-compose-build.yml --rm -e SERVICE_ENV=build svc-example node_modules/.bin/mocha tests'
  } finally {
    sh 'docker-compose -f down'
  }
  
  stage 'publish'
}
