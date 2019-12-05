pipeline {
  agent { docker { image 'circleci/android:api-23-node' } }
  stages {
    stage('build') {
      steps {
          sh './gradlew --no-daemon'
      }
    }
    stage('lint'){
      steps{
        script {
          try {
            sh './gradlew check'
          } catch (Exception e) {
            echo e.getMessage()
            echo "Lint failed"
          }
        }       
      }
      post {
        always {
            archiveArtifacts 'app/build/reports/**/*.xml'
            archiveArtifacts 'app/build/reports/**/*.html'
        }
      }
    }
    stage('test'){
      steps{
        script {
          try {
            sh './gradlew test'
          } catch (Exception e) {
            echo e.getMessage()
            echo "Release failed"
          }
        }       
      }
      post {
        always {
          archiveArtifacts 'app/build/reports/tests/**/*'
        }
      }
    }
  }
} 