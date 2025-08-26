pipeline {
  agent { label 'Jenkins-Agent' }
  tools {
    jdk 'Java17'
    maven 'Maven3'
    git 'Default-Git'  // Ensure this matches the name in Jenkins
  }
 // environment {
 //   JAVA_HOME = tool name: 'Java17', type: 'jdks'
 //   MAVEN_HOME = tool name: 'Maven3', type: 'maven'
 //   MAVEN_OPTS = '-Xmx1024m'
//  }
  stages {
    stage("Checkout from SCM") {
      steps {
        checkout scm  // Uses the repository configured in the Jenkins job
      }
    }
    stage("Build Application") {
      steps {
        sh "mvn clean package" || error "Build failed!"
      }
    }
    stage("Test Application") {
      steps {
        sh "mvn test" || error "Tests failed!"
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
      cleanWS()  // Clean up workspace after build
    }
    success {
      echo 'Build succeeded!'
      // Add notification steps (e.g., Slack, email)
    }
    failure {
      echo 'Build failed!'
      // Add notification steps (e.g., Slack, email)
    }
  }
}
