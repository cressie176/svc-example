node {
  wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'XTerm', 'defaultFg': 1, 'defaultBg': 2]) {
    stage 'checkout'
    checkout scm
  
    stage 'manifest'
    sh 'make-manifest --extra "build.number: ${BUILD_NUMBER}" --extra "build.url:${BUILD_URL}"'
  
    stage 'build'
    sh 'docker-compose -f docker/docker-compose-build.yml build svc-example'
  
    stage 'test'
    try {
      sh 'docker-compose -f docker/docker-compose-build.yml run --rm -e SERVICE_ENV=build svc-example bash -c \'sleep 5 && node_modules/.bin/mocha tests\''
    } finally {
      sh 'docker-compose -f docker/docker-compose-build.yml down'
    }
    
    stage 'publish'
    sh 'echo $GIT_COMMIT'
  }
}
