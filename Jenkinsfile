pipeline{
agent any

tools {
  maven 'mymvn'
}
  parameters {
  choice choices: ['dev', 'prod'], name: 'select_enviroment'
}

stages {

    stage('build') {
        steps {
            sh 'mvn clean package -DskipTests=true'
            }
     }
   stage('test') {
   parallel {
       stage('test A'){
         steps{
           echo 'test A'
           sh 'mvn test'
         }
       }
     
       stage('test B'){
       steps{
         echo 'test B'
         sh 'mvn test'
       }
     }
   }

     post {
  success {
    dir("target/"){
      stash name : "main-file", includes : "*.war"
    }
  }
}

     
  }


  stage('deploy_Dev'){
    when { expression {params.select_enviroment=='dev'}  beforeAgent true }
    // agent {
    //   lebel 'DevServer'
    // }
    agent any
    steps{
      dir("/home/azureuser/apache-tomcat-9.0.96/webapps"){
         unstash "main-file"
        
      }

      dir("/home/azureuser/apache-tomcat-9.0.96/bin"){
        sh './startup.sh'
      }
      
      
    }
  }


}

}
