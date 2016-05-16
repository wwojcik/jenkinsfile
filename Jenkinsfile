stage "Checkout"
node {
  checkout scm
}
stage "Build"
node {
    sh 'cp ./docker-compose.yml.dist ./docker-compose.yml'
    sh 'docker-compose build php'
    sh 'docker-compose run cli composer install'
}

