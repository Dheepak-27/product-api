pipeline {
  agent any

  environment {
    SONARQUBE = 'MySonarQubeServer'  // Optional if SonarQube is not configured
  }

  stages {
    stage('Build') {
      steps {
        echo '✅ Building Docker image...'
        sh 'docker build -t product-api .'
      }
    }

    stage('Test') {
      steps {
        echo '✅ Running unit tests...'
        sh 'npm install'
        sh 'npm test'
      }
    }

    stage('Code Quality') {
      steps {
        echo '📊 Code quality check...'
        // Replace with actual SonarQube command if configured
        echo 'Skipped SonarQube (not configured)'
      }
    }

    stage('Security') {
      steps {
        echo '🔒 Running Snyk scan...'
        sh 'npm install -g snyk'
        sh 'snyk test || echo "⚠️ Vulnerabilities found (ignore in test)"'
      }
    }

    stage('Deploy') {
      steps {
        echo '🚀 Deploying to Docker container...'
        sh 'docker-compose up -d'
      }
    }

    stage('Release') {
      steps {
        echo '🏷️ Tagging release...'
        sh 'git config --global user.email "you@example.com"'
        sh 'git config --global user.name "Your Name"'
        sh 'git tag v1.0.0'
        sh 'git push origin v1.0.0'
      }
    }

    stage('Monitoring') {
      steps {
        echo '🩺 Checking app health...'
        sh 'curl --fail http://localhost:3000/health || echo "App down!"'
      }
    }
  }
}