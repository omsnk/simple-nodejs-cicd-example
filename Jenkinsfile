pipeline {
  environment {
    VERCEL_PROJECT_NAME = 'learn-jenkins-app'
    VERCEL_TOKEN = credentials('devops26-vercel-token') // ดึงจาก Jenkins
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
    stage('Build') {
      steps {
        container('my-builder') {
          sh 'npm ci'
          sh 'npm run build'
        }
      }
    }

    stage('Test Build') {
      steps {
        container('my-builder') {
          sh 'npm run test'
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