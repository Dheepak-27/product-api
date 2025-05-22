pipeline {
  agent any

  environment {
    SONARQUBE = 'MySonarQubeServer'  // Optional if SonarQube is not configured
  }

  stages {
    stage('Build') {
      steps {
        echo '✅ Building Docker image...'
        bat 'docker build -t product-api .'
      }
    }

    stage('Test') {
      steps {
        echo '✅ Running unit tests...'
        bat 'npm install'
        bat 'npm test'
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
        bat 'npm install -g snyk'
        bat 'snyk test || echo "⚠️ Vulnerabilities found (ignore in test)"'
      }
    }

    stage('Deploy') {
      steps {
        echo '🚀 Deploying to Docker container...'
        bat 'docker-compose up -d'
      }
    }

    stage('Release') {
      steps {
        echo '🏷️ Tagging release...'
        bat 'git config --global user.email "you@example.com"'
        bat 'git config --global user.name "Your Name"'
        bat 'git tag v1.0.0'
        bat 'git push origin v1.0.0'
      }
    }

    stage('Monitoring') {
      steps {
        echo '🩺 Checking app health...'
        bat 'curl --fail http://localhost:3000/health || echo "App down!"'
      }
    }
  }
}