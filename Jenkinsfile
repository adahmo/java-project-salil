pipeline {
   environment {
     git_url = "https://github.com/adahmo/java-project-salil.git"
     git_branch = "master"
   }

  agent {label 'dev'}
  stages {
    stage('Pull Source') {
      steps {
        git credentialsId: 'fbc1c029-3786-421f-8866-38908874f70b', branch: "${git_branch}", url: "${git_url}"
       
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
                 withCredentials([usernamePassword(credentialsId: 'a06764d1-1d7c-43d4-9dd0-06bcb29c1723', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                //sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 //sh "sudo docker image tag myjava-image salilkul87/myjava-image:test"
                 //sh "sudo docker image tag myjava-image salilkul87/myjava-image:${BUILD_NUMBER}"
                 //sh "sudo docker image push salilkul87/myjava-image:${BUILD_NUMBER}" 
               } 
             }  
          }
      stage('Deploy app') {
         steps {
           sh 'ls -ltr'
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
