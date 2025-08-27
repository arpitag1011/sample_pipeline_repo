pipeline {
  agent {
    // Use Node.js in Docker so you don't need Node installed on Jenkins
    docker { image 'node:20-alpine' }
  }

  environment {
    CI = 'true'  // Tells create-react-app to run tests in CI mode
  }

  stages {
    stage('Checkout') {
      steps {
        echo '📥 Checking out source...'
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        echo '📦 Installing dependencies...'
        sh 'npm ci || npm install'
      }
    }

    stage('Test') {
      steps {
        echo '🧪 Running tests...'
        // CRA runs Jest tests; --watchAll=false makes it CI-friendly
        sh 'npm test -- --watchAll=false'
      }
    }

    stage('Build') {
      steps {
        echo '🔨 Building production bundle...'
        sh 'npm run build'
      }
    }

    stage('Archive Artifact') {
      steps {
        echo '📦 Archiving build output...'
        archiveArtifacts artifacts: 'build/**', fingerprint: true
      }
    }

    stage('Deploy (Demo)') {
      steps {
        echo '🚀 Deploying (demo to workspace/deploy)...'
        sh '''
          rm -rf deploy && mkdir -p deploy
          cp -r build/* deploy/
          echo "Deployed locally to $PWD/deploy (demo). Replace this with real server upload later."
        '''
      }
    }
  }

  post {
    success { echo '✅ Pipeline executed successfully!' }
    failure { echo '❌ Pipeline failed. Check logs.' }
  }
}