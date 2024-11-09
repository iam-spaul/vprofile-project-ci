pipeline {
    agent any

    tools {
        maven 'mymvn'
    }

    parameters {
        choice choices: ['dev', 'prod'], name: 'select_environment'
    }

    stages {
        stage('build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }

//    stage('test') {
//    parallel {
//        stage('test A'){
//          steps{
//            echo 'test A'
//            sh 'mvn test'
//          }
//        }
     
//        stage('test B'){
//        steps{
//          echo 'test B'
//          sh 'mvn test'
//        }
//      }
//    }

//      post {
//   success {
//     dir("target/"){
//       stash name : "vp", includes : "*.war"
//     }
//   }
// }

     
//   }

//  stage('deploy_Dev') {
//     when {
//         beforeAgent true
//         expression { params.select_environment == 'dev' }
//     }
//     agent any
//     steps {
//         script {
//             sh 'pwd && ls -la /home/azureuser/tomcatserver/webapps'
//             def dirExists = fileExists('/home/azureuser/tomcatserver/webapps')
//             if (dirExists) {
//                 dir('/home/azureuser/tomcatserver/webapps') {
//                     sh 'echo "Changed directory to webapps and running commands here."'
//                 }
//             } else {
//                 error("Directory does not exist: /home/azureuser/tomcatserver/webapps")
//             }
//         }
//     }
// }
        stage('dev'){
            steps{
                sh 'ls -la /home/azureuser/tomcatserver/webapps'

            }
        }


    }
}
