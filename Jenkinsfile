pipeline {
  agent { label 'Jenkins-Agent' }
  tools {
    jdk 'Java17'
    maven 'Maven3'
    git 'Default-git'
  }
  stages{
    stage("Cleanup Workspace"){
      steps{
        cleanWS()
      }
    }

    stage("Checkout from SCM"){
      steps {
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/Mirza-1W/registration-app'
      }
    }

    stage("Build Application"){
      steps {
        sh "mvn clean package"
      }
    }

    stage("Test Application"){
      steps {
        sh "mvn test"
      }
    }
  }
}
