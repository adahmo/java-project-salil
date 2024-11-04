pipeline {
   environment {
     git_url = "https://github.com/adahmo/java-project-salil.git"
     git_branch = "master"
   }

  agent {label 'dev'}
  stages {
    stage('Pull Source') {
      steps {
        git credentialsId: 'dfb0a627-ed77-4e0d-adf8-ada326a74efc', branch: "${git_branch}", url: "${git_url}"
       
      }
     }
    
    stage('Maven Build') {
     steps { 
          sh "mvn clean package && cp target/*.jar . "
     }
    }
     
    stage('Docker Image Build') {     
        steps {
            sh 'sudo docker build -t myjava-image . '
               }
             }
        stage('Docker image push') {
           steps {
                 withCredentials([usernamePassword(credentialsId: '9a057081-4008-40a0-8757-1dd9d3a5b511', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                 sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 sh "sudo docker image tag myjava-image adamumj/myjava-image:test"
                 sh "sudo docker image tag myjava-image adamumj/myjava-image:${BUILD_NUMBER}"
                 sh "sudo docker image push adamumj/myjava-image:${BUILD_NUMBER}" 
               } 
             }  
          }
      stage('Deploy app') {
         steps {
           sh 'ls -lta'
           //sh 'kubectl apply -f app-deploy.yaml'
            // sh 'sudo docker container run -d --name testcont salilkul87/myjava-image:test'
        }
     }
    }

//  post {
//    always {
//      deleteDir() /* cleanup the workspace */
//    }
//  }
 }
