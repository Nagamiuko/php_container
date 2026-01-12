pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/Nagamiuko/php_container.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t php-app:latest .'
      }
    }

    stage('Test') {
      steps {
        sh '''
          echo "Run tests here"
          # vendor/bin/phpunit
        '''
      }
    }

    stage('Deploy') {
      steps {
        sh '''
          docker stop php-app || true
          docker rm php-app || true
          docker run -d \
            --name php-app \
            -p 8080:80 \
            my-php-app:latest
        '''
      }
    }
  }
}
