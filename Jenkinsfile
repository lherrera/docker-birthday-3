node ('ci-docker') {
 stage "Checkout App Code"
  checkout scm
  dir ('example-voting-app') {
   stage "Build Images"
     sh "docker-compose build"
     sh "docker push lherrera/voting-app"
     sh "docker push lherrera/result-app"

   stage "Deploy Application on CI env"
     sh "docker-compose  stop"
     sh "docker-compose  rm -f"
     sh "docker-compose  up -d"
   stage "Test" 
	parallel 'integration': {
          sh "sleep 10"
          sh "curl localhost:5000"
          sh "curl localhost:5001"
        },
        'quality': {
          echo "always missing"
        }
   stage "Publish Application Details"
    sh "docker-compose ps"
   stage "Permiso?"
    timeout(time: 7, unit: 'DAYS') {
    input message: 'Do you want to deploy?'}
  }
}
node ('prod') {
  checkout scm
  dir ('example-voting-app') {
    stage "Deploying in production"
    sh "docker-compose -f docker-compose.prod.yml up -d"
  }
}

