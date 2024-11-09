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
                stage('test A') {
                    steps {
                        echo 'test A'
                        sh 'mvn test'
                    }
                }
                stage('test B') {
                    steps {
                        echo 'test B'
                        sh 'mvn test'
                    }
                }
            }
        }

        stage('stash war file') {
            when { branch 'main' }
            post {
                success {
                    dir("target/") {
                        stash name: "vp", includes: "*.war"
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
                dir("target/deploy") {
                    unstash "vp"
                }
                dir("/apache-tomcat-9.0.96/bin") {
                    sh './startup.sh'
                }
            }
        }
    }
}
