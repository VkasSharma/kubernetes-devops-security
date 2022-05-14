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
        steps {
        sh "mvn test"
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco execPattern: 'target/jacoco.exec'
        }
      }
      } 

      stage('Docker Build and Push') {
      steps {
        withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
          sh 'printenv'
          sh 'docker build -t vikaspramila/devsecops:""$GIT_COMMIT"" .'
          sh 'docker push vikaspramila/devsecops:""$GIT_COMMIT""'
        }
      }
    }    
    }
}