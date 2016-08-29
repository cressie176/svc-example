node {
  wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'XTerm', 'defaultFg': 1, 'defaultBg': 2]) {
    stage 'checkout'
    checkout scm

    stage 'manifest'
    sh 'make-manifest --extra "build.number: ${BUILD_NUMBER}" --extra "build.url: ${BUILD_URL}"'
  
    stage 'build'
    sh 'docker-compose -f docker/docker-compose-build.yml build svc-example'
  
    stage 'test'
    try {
      sh 'docker-compose -f docker/docker-compose-build.yml run --rm -e SERVICE_ENV=build svc-example sleep 5'
      sh 'docker-compose -f docker/docker-compose-build.yml run --rm -e SERVICE_ENV=build svc-example node_modules/.bin/mocha'
    } finally {
      sh 'docker-compose -f docker/docker-compose-build.yml down'
    }
    
    stage 'publish'
    sh 'docker tag quay.io/guidesmiths/svc-example:latest quay.io/guidesmiths/svc-example:$(git rev-parse HEAD)'
  }
}
