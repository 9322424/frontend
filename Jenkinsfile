pipeline {
  agent {
    docker {
      image 'schoolofdevops/node:4-alpine'
    }

  }
  stages {
    stage('build') {
      agent {
        docker {
          image 'schoolofdevops/node:4-alpine'
        }

      }
      steps {
        echo 'this is the build job'
        sh 'npm install'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'schoolofdevops/node:4-alpine'
        }

      }
      steps {
        echo 'this is the test job'
        sh 'npm test'
      }
    }

    stage('package') {
      agent {
        docker {
          image 'schoolofdevops/node:4-alpine'
        }

      }
      steps {
        echo 'this is the package job'
        sh 'npm run package'
        archiveArtifacts '**/distribution/*.zip'
      }
    }

    stage('capstone build and publish') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("9322424/frontend:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
          }
        }

      }
    }

  }
  post {
    always {
      echo 'this pipeline has completed...'
    }

  }
}