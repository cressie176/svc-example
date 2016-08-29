node {
  stage 'env'
  env.each{ k, v -> println "${k}:${v}" }
  
  stage 'build'

  stage 'test'
  
  stage 'publish'
}
