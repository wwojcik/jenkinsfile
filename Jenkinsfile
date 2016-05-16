node {
stage "Checkout"
  checkout scm
stage "Build"
  sh 'ls'
  sh 'cp ./docker-compose.yml.dist ./docker-compose.yml'
  sh 'docker-compose build php'
  sh 'docker-compose run cli composer install'
}
