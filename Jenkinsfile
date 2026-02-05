pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: my-builder
    image: node:20-alpine
    command:
    - cat
    tty: true
"""
    }
  }

  stages {
    stage('Install') {
      steps {
        container('my-builder') {
          sh 'npm ci'
        }
      }
    }

    stage('Check') {
      steps {
        container('my-builder') {
          sh 'node --version'
          sh 'npm --version'
        }
      }
    }
  }
}
