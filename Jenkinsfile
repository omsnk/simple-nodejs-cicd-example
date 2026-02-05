pipeline {
  environment {
    VERCEL_PROJECT_NAME = 'learn-jenkins-app'
    VERCEL_TOKEN = credentials('devops26-vercel-token')
  }

  agent {
    kubernetes {
      yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: my-builder
    image: node:20-alpine
    command:
    - cat
    tty: true
'''
    }
  }

  stages {

    stage('Test npm') {
      steps {
        container('my-builder') {
          sh 'node --version'
          sh 'npm --version'
        }
      }
    }

    stage('Install Dependencies') {
      steps {
        container('my-builder') {
          sh 'npm ci'
        }
      }
    }

    stage('Test') {
      steps {
        container('my-builder') {
          sh 'npm test || echo "No tests defined"'
        }
      }
    }

    stage('Deploy') {
      steps {
        echo 'deploy step (placeholder)'
      }
    }
  }
}
