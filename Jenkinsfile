pipeline {
  agent {
    docker {
      image "node:alpine"
      args "--network=skynet"
    }
  }
  stages {    
    stage("Build") {
      steps {
        sh "apk upgrade --update"
        sh "apk add --no-cache mongodb \
           --repository http://dl-cdn.alpinelinux.org/alpine/v3.9/main \
           --repository http://dl-cdn.alpinelinux.org/alpine/v3.9/community"
        sh "chmod +x ./scripts/dropdb.sh"
        sh "npm install"
      }
    }
    stage("Test") {
      steps {
        sh "npm run test:ci"
      }
      post {
        always {
          junit "log/*.xml"
        }
      }
    }
    stage("Production") {
      steps {
        input message: "Go to production? (Clik 'Proceed' to continue)"
        sh "echo 'subindo em produção'"
      }
    }
  }
}
