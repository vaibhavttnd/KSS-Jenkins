pipeline {
  agent {
    docker {
      image 'maven:3-jdk-8'
    }
    
  }
  stages {
    stage('User Confirmation') {
      steps {
        input 'Proceed or Abort'
      }
    }
    stage('Git checkout') {
      steps {
        git(url: 'https://github.com/vaibhavttnd/KSS-Jenkins.git', credentialsId: '93232a53-4af3-40d7-b2c7-b7c15a45f879', branch: 'master', changelog: true, poll: true)
      }
    }
    stage('Test Cases') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Build Artifacts') {
      steps {
        when {
                expression { env.GIT_BRANCH == 'staging' } 
        }
        steps {
           sh 'mvn package'
        }
         when {
                expression { env.GIT_BRANCH == 'staging' } 
        }
         steps {
             lock('myResource') {
    echo "locked build"
  }
        }
      }
    }
  }
}
