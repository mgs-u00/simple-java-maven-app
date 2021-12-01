pipeline {
  agent {
    docker {
      image 'maven:3.8.1-adoptopenjdk-11' //1
      args '-v /root/.m2:/root/.m2' //2
    }
  }
  options {
    skipStagesAfterUnstable()
  }
  stages {
    stage('Build') { //3
      steps {
        sh 'mvn -B -DskipTests clean package' //4
      }
    }
  stage('Test') {
    steps {
      sh 'mvn test'
    }
    post {
      always {
        junit 'target/surefire-reports/*.xml'
      }
    }
  }
  stage('Send') { //1
    steps {
    sh './jenkins/scripts/deliver.sh' //2
}
}
}
}
