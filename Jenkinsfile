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
      stash name : "vp", includes : "*.war"
    }
  }
}

     
  }

       stage('deploy_Dev') {
    when {
        beforeAgent true
        expression { params.select_environment == 'dev' }
    }
    agent any
    steps {
        script {
            def dirExists = fileExists('/home/azureuser/apache-tomcat-9.0.96/webapps')
            if (dirExists) {
                sh 'cd /home/azureuser/apache-tomcat-9.0.96/webapps && echo "Changed directory to webapps"'
            } else {
                error("Directory does not exist: /home/azureuser/apache-tomcat-9.0.96/webapps")
            }
        }
    }
}

    }
}
