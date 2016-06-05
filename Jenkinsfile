node ('docker') {
 stage "Checkout App Code"
  checkout scm
  dir ('example-voting-app') {
   stage "Build Images"
     sh "docker-compose build"
   stage "Deploy Application"
     sh "docker-compose  stop"
     sh "docker-compose  rm -f"
     sh "docker-compose  up -d"
   stage "Testing"
    sh "sleep 10"
    sh "curl localhost:5000"
    sh "curl localhost:5001"
   stage "Publish Application Details"
    sh "docker-compose ps"
 }
}
