node {
  // Fix terminal colours
  wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'XTerm', 'defaultFg': 1, 'defaultBg': 2]) {
    
    stage 'checkout'
    checkout scm

    // Requires make-manifest npm module to be installed globally on the jenkins host
    stage 'manifest'
    sh 'make-manifest --extra "build.number: ${BUILD_NUMBER}" --extra "build.url: ${BUILD_URL}"'
  
    stage 'build'
    // Builds the service from the docker-compose build file. We use a separate docker-compose 
    // file for CI so the netork is isolated to just this project. Locally we share  
    // dependencies over the 'local' network
    sh 'docker-compose -f docker/docker-compose-build.yml build svc-example'
  
    stage 'test'
    try {
      // Run the service container (which starts all the dependencies)
      // We execute sleep since it takes postgres a while to startup
      sh 'docker-compose -f docker/docker-compose-build.yml run --rm -e SERVICE_ENV=build svc-example sleep 5'
      
      // Run the service container again, this time executing the tests
      sh 'docker-compose -f docker/docker-compose-build.yml run --rm -e SERVICE_ENV=build svc-example node_modules/.bin/mocha tests'
    } finally {
      
      // Shutdown all the dependencies (service container was automatically removed with --rm)
      sh 'docker-compose -f docker/docker-compose-build.yml down'
    }
    
    stage 'publish'
    // Tag the image with the git commit sha
    sh 'docker tag quay.io/guidesmiths/svc-example:latest quay.io/guidesmiths/svc-example:$(git rev-parse HEAD)'
    
    // Publish the image and all it's tasgs to the repo
    sh 'docker push quay.io/guidesmiths/svc-example'
  }
}
