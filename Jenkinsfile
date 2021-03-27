pipeline {
  agent any
  options {
    timestamps();
  }

  stages {

    stage('checkout') {
      steps {
        checkout scm
      }
    }

    stage('setup') {
      steps {
        sh """
          autoreconf --verbose --install --force
          ./configure
        """
      }
    }

    stage('build') {
      steps {
        sh """
          make all
          make dist
        """
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: 'sub*.tar.gz', onlyIfSuccessful: true
      step([$class: 'WsCleanup'])
    }
  }
}
