pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so  can be downloaded later
            }
        }
      stage ('Unit Test'){
        sh 'mvn test'
      }     
    }
}